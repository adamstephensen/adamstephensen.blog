---
title: What skills do you need to have on your tool-belt to be a great .Net developer?
permalink: /2014/05/04/what-skills-do-you-need-to-have-on-your-tool-belt-to-be-a-great-net-developer/
layout: post
tags:
  - .NET
comments: true
---

This is what I consider to be my list of 'essential' tools / skills for a serious .Net developer.
<h2>An Agile or Lean methodology</h2>
<h4>Learn Scrum</h4>
If your projects are not being delivered successfully Scrum will either enable you to start delivering software, or highlight the reasons why you aren't.
The Scrum Guide which contains all the rules of Scrum is 13 pages long. There is no excuse for not having read it.
If you aren't doing Scrum, or you aren't doing it well… get some help.
<h2>ALM</h2>
<h4>Learn TFS</h4>
Out of the box, it gives you so much. I find it incredible how many people have TFS but are only using it for Source Control.
<h4>Source Control</h4>
Learn both Team Foundation Source Control and Git, and the strengths of each.
<h4>Work Item Tracking</h4>
Being able to successfully deliver value to the customer while triaging bugs requires efficient work item tracking processes and tools.
<h4>Continuous Integration</h4>
Why-oh-why isn't everyone doing CI?
Check in your code, have a magic fairy build it, test it and tell you if you've broken anything - sounds too good to be true AND it only takes 60 seconds to setup!
'Fail Fast' is probably my favourite development catch-phrase: If you find out that the code you've just checked-in conflicts with some-one else’s code 2 minutes after you've checked it in, it's easy to resolve the issue. If you only find out there is an issue a week later, it's much harder.
<h4>Deployment:</h4>
Get your CI fairy to take the code she builds and then deploy it to a server for you.
If every time you finish a task you can send the user a link to the test server that you just deployed to and say 'tell me what you think'. The customer will LOVE you… and you get feedback when it's most helpful.
If you are using Azure, continuous deployment is just so damn easy.
Also, I am having a little love affair with a tool called Octopus Deploy <a href="http://www.octopusdeploy.com" target="_blank">http://www.octopusdeploy.com</a>. Check it out!
<h2>Cloud</h2>
As a .Net guy… you need to be familiar with Azure.
It's remarkable how easy it has become to build and deploy web applications to the cloud. In 30 minutes I can create a source code repository on <a href="http://visualstudio.com" target="_blank">http://visualstudio.com</a>, check in an MVC project and have it continuously deploying to an Azure website with both Release and Staging environments.
<a href="http://firebootcamp.com/windows-azure-websites-quickstart-andrew-coates/" target="_blank">Check out Andrew Coates from Microsoft doing continuous deployment to Azure at FireBootCamp.</a>

Azure is so much more than just websites… but as this is a 'need to know' list, I'll force myself to not go on about how awesome Azure VMs and Web Roles are. If you take an interest in the cloud, Azure is a platform that will have you boring all your friends with tales of how cool it is.
<h2>Communication</h2>
Communication and interpersonal skills cannot be overemphasised. No matter how smart someone is, you don't want them on your team if they can't work as part of the team.
<ul>
	<li>You need to know how to take instructions</li>
	<li>You need to know how to provide feedback</li>
	<li>You need to know how and when to push back, and when to give in</li>
	<li>Sometimes, you just need to shut-up</li>
</ul>
<h2>Patterns, Practices and Principles.</h2>
This is the stuff I'm REALLY passionate about.

Building a complex application, that is still going to be maintainable after you have added features to it for several years requires some skills. My mission is to increase the understanding amongst .Net developers that the following are essential, not hard to learn, will improve your job satisfaction and your employers opinion of you when you continue to add value to his application well after other projects have ground to a halt.
<h4>Dependency Injection</h4>
This is *not* about swapping your SQL Database for an Oracle one!

There are many, many benefits to Dependency Injection: Here is the major one for me - you need dependency injection to ensure that your complex system is built in such a way that changes to one module does not cause flow on effects in other modules.

Typical on many projects: first 10 features get thrown together in a week, the next 10 features take 2 weeks, the next 10 take a month, and then every subsequent feature takes longer and longer because of the changes that need to be made throughout the project to implement the new features.
<blockquote>Dependency Injection is about ensuring you can continue to add features to your complex project.</blockquote>
<h4><span style="font-weight:normal;">Essential Reading: <a href="http://www.amazon.com/Dependency-Injection-NET-Mark-Seemann/dp/1935182501" target="_blank">Dependency Injection in .Net by Mark Seeman</a></span></h4>
<h4>Unit Testing</h4>
I’m not a code coverage guy. I don’t believe every single line of code needs a unit tests.

I believe the following
<blockquote><span style="color:#444444;">You NEED to be able to write great tests.
Your application should have unit tests over 100% of the code that requires unit tests.</span></blockquote>
This is a topic that I can (and do) talk about for hours, but in summary:

I write tests

- for fragile code, or code that is likely to break

- for important code that you cannot afford to break

- for code that is hard to read: Well written unit tests are the best form of documentation after well written code.

- when writing the test provides me clarity about the code that I am about to write (slipped my TDD hat on there for a minute)

and

- When writing a unit test will save my boss money because it’s faster than the (damn) debugger

One of my favourite rants: It is often faster to write a unit test than to test the code you have just written any other way.

I see this a lot and it drives me crazy: I’m testing the credit card validation of my online store. I want to test the submitted card number against a regex before I submit it to the Bank.

Debugger Guy: I hit F5, wait for the whole solution to compile, the website to spin up and the debugger to attach. I then select several items to add to my cart, click next, enter my name, phone number and address, click next, enter the credit card number and click next, realise there is a typo in the Regex, click Stop, change one character and press F5 again ! aaaaaarrrrggghhh !

Unit Test Guy: Writes a 5 line unit test in half the time it takes Debugger guy to even reach the code, gets feedback in milliseconds, provides great documentation about what the regex is validating and ensures that changes to the code in the future do not invalidate the current requirements.

Essential reading: <a href="http://www.amazon.com/The-Art-Unit-Testing-examples/dp/1617290890/ref=dp_ob_title_bk" target="_blank">The Art of Unit Testing by Roy Osherove</a>

My session on unit testing: <a href="http://tv.ssw.com/2781/eat-your-vegetables-unit-tests-dependency-injection-adam-stephensen" target="_blank">Eat your vegetables! Baking Healthy Projects with Unit Testing and Dependency Injection</a>
<h4>Common patterns like Repository and Unit of Work</h4>
Patterns are important.

They provide a way for developers to communicate about common problems and suggested solutions.

I hate to re-invent the wheel when smarter people have already come before me and done most of the heavy lifting.

Familiarity with common patterns (the good and the bad) is essential to any senior developer.
<h4>Clean Code & SOLID Principles</h4>
If software were disposable, I wouldn’t be writing this post.

If I could write software today, and then walk away and never have to look at it again I may not care about the day next year when I have to come back and make sense of it – but I do.

Because I have to maintain my code – I should very much care about making it easy to maintain. This is where the idea of ‘Clean Code’ and the SOLID Principles come in.

Essential reading: <a href="http://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882" target="_blank">Clean Code by Robert Martin</a>

Professional developers should be proud of the code they write.

 

I struggle to understand why most developers still don’t have a good understanding of the above topics. I strongly believe that these areas should be lived and breathed by every member of a development team.
Once again, you don't have to always use them… but if you don't have them in your tool-belt you're selling yourself as a professional carpenter when you don't even own a hammer.
<h2>Technologies</h2>
I've deliberately left this until last.

Although most job descriptions are full of technologies, I believe that knowledge of the topics above are far more important.

Here is the current set of technologies that we use by default to build most of our web applications.
<ul>
	<li>Obviously C#, HTML, JavaScript and jQuery.</li>
</ul>
<ul>
	<li>Frameworks and Toolsets-> we like to keep across what's out there, and being consultants doing new projects all the time we get to try out different things but our default stack at the moment is
<ul>
	<li>Twitter Bootstrap</li>
	<li>Angular.js</li>
	<li>Telerik KendoUI</li>
	<li>SignalR</li>
</ul>
</li>
</ul>
<h2>Summary</h2>
I deliver large, high performing web applications for enterprises. The processes, tools and technologies above are what I believe an enterprise web developer needs to know. Obviously other development disciplines require very different skills sets.

In many scenarios other tools, frameworks or methods may be more appropriate, but before you start learning all the alternatives you should know and understand the mainstream choice. Then you are qualified to have an opinion about whether something else is better.

