---
title: Understanding the Enterprise Bot Template (draft)
layout: post
tags:
  - Azure
  - AI
  - Bots
  - Cognitive Services
comments: true
---
# Understanding the Enterprise Bot Template

This is my version of the [how bots work](
https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&tabs=cs) doco page,  customised to explain the Enterprise Bot Template. 

The reason that I have done my own version is that for me I'd rather read well commented (overly commented) code to understand how something works than reading a paragraph of text, then associating it with code.

## Sources
- [how bots work](
https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&tabs=cs)

### Bot Class

``` C#
class EchoWithCounterBot : IBot
** todo: check this
```

- The main bot logic is defined in the EchoWithCounterBot class that derives from the IBot interface. 
- IBot defines a single method OnTurnAsync. 

### OnTurnAsync


``` C#
public async Task OnTurnAsync(ITurnContext turnContext, CancellationToken cancellationToken = default(CancellationToken)) 
```


OnTurnAsync: updated with my code comments. I wouldn't usually write this many comments in code ;-)

``` C#
// Turncontext provides information about the incoming activity. 
	public async Task OnTurnAsync(ITurnContext turnContext, CancellationToken cancellationToken = default(CancellationToken))
{

	//The incoming activity corresponds to the inbound HTTP request. 
	// Activities can be of various types, so we check to see if the bot has received a message. 
    if (turnContext.Activity.Type == ActivityTypes.Message)
    {
		//If it is a message, we get the conversation state from the turn context, increment the turn counter, and then persist the new turn counter value into the conversation state. 

        // Get the conversation state from the turn context.
        var oldState = await _accessors.CounterState.GetAsync(turnContext, () => new CounterState());

        // Bump the turn count for this conversation.
        var newState = new CounterState { TurnCount = oldState.TurnCount + 1 };

        // Set the property using the accessor.
        await _accessors.CounterState.SetAsync(turnContext, newState);

        // Save the new turn count into the conversation state.
        await _accessors.ConversationState.SaveChangesAsync(turnContext);


		// And then send a message back to the user using SendActivityAsync call. 
		// The outgoing activity corresponds to the outbound HTTP request.

        // Echo back to the user whatever they typed.
        var responseMessage = $"Turn {newState.TurnCount}: You sent '{turnContext.Activity.Text}'\n";
        await turnContext.SendActivityAsync(responseMessage);
    }
    else
    {
        await turnContext.SendActivityAsync($"{turnContext.Activity.Type} event detected");
    }
}
```

## Set up services

The ConfigureServices method in the startup.cs file 
- is where [.NET Core configure Dependency Injection as per the docs](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-2.2)
- it loads the connected services from .bot file, 
- catches any errors that occur during a conversation turn and logs them,
- sets up your credential provider and 
- creates a conversation state object to store conversation data in memory.

``` C#
services.AddBot<EchoWithCounterBot>(options =>
{
    // Creates a logger for the application to use.
    ILogger logger = _loggerFactory.CreateLogger<EchoWithCounterBot>();

    var secretKey = Configuration.GetSection("botFileSecret")?.Value;
    var botFilePath = Configuration.GetSection("botFilePath")?.Value;

    // Loads .bot configuration file and adds a singleton that your Bot can access through dependency injection.
    BotConfiguration botConfig = null;
    try
    {
        botConfig = BotConfiguration.Load(botFilePath ?? @".\BotConfiguration.bot", secretKey);
    }
    catch
    {
        //...
    }

    services.AddSingleton(sp => botConfig);

    // Retrieve current endpoint.
    var environment = _isProduction ? "production" : "development";
    var service = botConfig.Services.Where(s => s.Type == "endpoint" && s.Name == environment).FirstOrDefault();
    if (!(service is EndpointService endpointService))
    {
        throw new InvalidOperationException($"The .bot file does not contain an endpoint with name '{environment}'.");
    }

    options.CredentialProvider = new SimpleCredentialProvider(endpointService.AppId, endpointService.AppPassword);

    // Catches any errors that occur during a conversation turn and logs them.
    options.OnTurnError = async (context, exception) =>
    {
        logger.LogError($"Exception caught : {exception}");
        await context.SendActivityAsync("Sorry, it looks like something went wrong.");
    };

    // The Memory Storage used here is for local bot debugging only. When the bot
    // is restarted, everything stored in memory will be gone.
    IStorage dataStore = new MemoryStorage();

    // ...

    // Create Conversation State object.
    // The Conversation State object is where we persist anything at the conversation-scope.
    var conversationState = new ConversationState(dataStore);

    options.State.Add(conversationState);
});
```

### Startup.cs - configuring state
Note: this is different to the getting started doc. It works differently in the enterprise template - we aren't configuring the stateaccessors in the ConfigureServices method

[Understanding state](https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-howto-v4-state?view=azure-bot-service-4.0&tabs=csharp)


``` C#

var dataStore = new CosmosDbStorage(cosmosOptions);
            var userState = new UserState(dataStore);
            var conversationState = new ConversationState(dataStore);

            services.AddSingleton(dataStore);
            services.AddSingleton(userState);
            services.AddSingleton(conversationState);
            services.AddSingleton(new BotStateSet(userState, conversationState));


```

### startup.cs - Configure method

The Configure method finishes the configuration of your app by specifying that the app use the Bot Framework and a few other files. All bots using the Bot Framework will need that configuration call. ConfigureServices and Configure are called by the runtime when the app starts.

``` C#
        public void Configure(IApplicationBuilder app, IHostingEnvironment env)
        {
            if (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }

            app.UseBotApplicationInsights()
                .UseDefaultFiles()
                .UseStaticFiles()
                .UseBotFramework();
        }
```		

## The bot file

The .bot file contains information, including the endpoint, app ID, and password, and references to services that are used by the bot. This file gets created for you when you start building a bot from a template, but you can create your own through the emulator or other tools. You can specify the .bot file to use when testing your bot with the emulator.

``` JSON
{
    "name": "echobot-with-counter",
    "services": [
        {
            "type": "endpoint",
            "name": "development",
            "endpoint": "http://localhost:3978/api/messages",
            "appId": "",
            "appPassword": "",
            "id": "1"
        }
    ],
    "padlock": "",
    "version": "2.0"
}
```

## State

```
- User state is available in any turn that the bot is conversing with that user on that channel, regardless of the conversation
- Conversation state is available in any turn in a specific conversation, regardless of user (i.e. group conversations)
- Private conversation state is scoped to both the specific conversation and to that specific user
```
Source: [Managing State](https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-concept-state?view=azure-bot-service-4.0)


``` C#


    public class OnboardingDialog : EnterpriseDialog
    {
        private static OnboardingResponses _responder = new OnboardingResponses();
        private IStatePropertyAccessor<OnboardingState> _accessor;
        private OnboardingState _state;

        public OnboardingDialog(BotServices botServices, IStatePropertyAccessor<OnboardingState> accessor, IBotTelemetryClient telemetryClient)
            : base(botServices, nameof(OnboardingDialog))
        {
            _accessor = accessor;
            InitialDialogId = nameof(OnboardingDialog);

            var onboarding = new WaterfallStep[]
            {
                AskForName,
                AskForEmail,
                AskForLocation,
                FinishOnboardingDialog,
            };

            // To capture built-in waterfall dialog telemetry, set the telemetry client 
            // to the new waterfall dialog and add it to the component dialog
            TelemetryClient = telemetryClient;
            AddDialog(new WaterfallDialog(InitialDialogId, onboarding) { TelemetryClient = telemetryClient });
            AddDialog(new TextPrompt(DialogIds.NamePrompt));
            AddDialog(new TextPrompt(DialogIds.EmailPrompt));
            AddDialog(new TextPrompt(DialogIds.LocationPrompt));
        }

        public async Task<DialogTurnResult> AskForName(WaterfallStepContext sc, CancellationToken cancellationToken)
        {
            _state = await _accessor.GetAsync(sc.Context, () => new OnboardingState());

            if (!string.IsNullOrEmpty(_state.Name))
            {
                return await sc.NextAsync(_state.Name);
            }
            else
            {
                return await sc.PromptAsync(DialogIds.NamePrompt, new PromptOptions()
                {
                    Prompt = await _responder.RenderTemplate(sc.Context, sc.Context.Activity.Locale, OnboardingResponses.ResponseIds.NamePrompt),
                });
            }
        }

```

## Dialogues

See [the dpcs](https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-concept-dialog?view=azure-bot-service-4.0)

[Gathering user input via Dialogues](https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-prompts?view=azure-bot-service-4.0&tabs=csharp)