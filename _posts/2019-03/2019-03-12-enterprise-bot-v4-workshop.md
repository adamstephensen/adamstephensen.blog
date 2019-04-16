---
title: Enterprise Bot Workshop Agenda (draft)
layout: post
bigimg:
  - /assets/images/angular-superpower-photo-1.jpg
tags:
  - Azure
  - AI
  - Bots
  - Cognitive Services
comments: true
---
# Enterprise Bot Workshop Agenda (draft)

This is a draft agenda for the bot workshops that Valeriia and I run with our customers.

I intend to flesh this out and improve it as we run more and more. 

## Demo of the Enterprise Bot Template

- **todo** Deploy Bot Template to Azure as per [Enterprise Bot Template - Getting Started](https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-enterprise-template-getting-started)

- **todo** Write Demo Script

## Enterprise Bot Template Architecture Discussion

## Intro to LUIS

- configure global LUIS Intents
- configure app specific LUIS Intents

## Intro to QnA Maker

- configure global QnA Maker
- configure app specific QnA Maker

## Intro to the Dispatcher

- wiring together the LUIS & QnA Maker docs

## Installing the Enterprise Bot Template

- [Docs](https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-enterprise-template-getting-started?view=azure-bot-service-4.0)

## Deploying the Enterprise Bot Template

[Deploying your bot](https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-enterprise-template-getting-started?view=azure-bot-service-4.0#deploy-your-bot)

## Customise the Enterprise Template

[Customise the template](https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-enterprise-template-customize?view=azure-bot-service-4.0)

- Review Project Structure
- Update Intro Message
- Update Bot Responses
- (skip updating cognitive models - already done)
- Add a new dialog

## View bot analytics & Telemetry

- [Cofigure analytics](https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-enterprise-template-getting-started?view=azure-bot-service-4.0#view-your-bot-analytics)

## Code inspection

- Typing indicators
- Language support
- Transcripts

## Consuming external APIs

## Configure Authentication

# Navigation
- images from https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-concept-dialog?view=azure-bot-service-4.0

## Resources: 

# Getting Ready 

## Setup Requirements

The requirements for the Enterprise Bot Template (as per https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-enterprise-template-deployment?view=azure-bot-service-4.0 )

Enterprise Template Bots require the following dependencies for end to end operation.

- Azure Web App
- Azure Storage Account (Transcripts)
- Azure Application Insights (Telemetry)
- Azure CosmosDb (Conversation State storage)
- Azure Cognitive Services - Language Understanding
- Azure Cognitive Services - QnA Maker (includes Azure Search, Azure Web App)
- Azure Cognitive Services - Content Moderator (optional manual step)

## Deploy the Enterprise Template before the workshop

Because the workshop covers a lot of ground, it is best if before the workshop a developer on the project follows the Create, Customise and Deploy steps for the bot template. 

The instructions are very straight forward and clear. Once this is done – in the workshop we can spend time explaining the code and best practices as opposed to going through the exact steps in the doco.

-	Create the project https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-enterprise-template-create-project?view=azure-bot-service-4.0
-	Customer the template https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-enterprise-template-customize?view=azure-bot-service-4.0 
-	Deploy the template https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-enterprise-template-deployment?view=azure-bot-service-4.0 

I’m looking forward to building a bot together !

