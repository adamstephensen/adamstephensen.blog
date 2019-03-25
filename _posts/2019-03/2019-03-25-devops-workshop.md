---
title: Azure DevOps Pipelines Workshop - Demo Scripts (Drafts)
permalink: 2019/03/25/azure-pipelines-workshop-demo-scripts/
layout: post
tags:
  - Azure
  - DevOps
comments: true
---

Source: https://www.azuredevopslabs.com/labs/azuredevops/continuousdeployment/

# #1 Embracing Continuous Delivery with Azure Pipelines

## Task 1 Setting up Azure Resources
- create a SQL Database
```
  database name: partsunlimited
  source: blank database
  server name: <yourname>-partsunlimited
```
- create a web app
```
  app name: <yourname>-partsunlimited-qa
  resource group & subscription: same as previous
  app service plan: accept the defaults
  OS: Windows
  Apop Insights: Off
```

## Task 2: Creating a continuous release to the QA state
- open a new browser tab for Azure DevOps https://dev.azure.com/YOURACCOUNT/Parts%20Unlimited.
- Navigate to Pipelines | Releases
- Delete the existing PartsUnlimitedE2E release pipeline
- Create a new release pipeline
```
template: Azure App Service Deployment
default stage: QA
pipeline name: PUL-CICD
artifact: Build | PartsUnlimitedE2E
QA environment task | select QA web app
```
- Turn on CI trigger
- Add a build branch trigger > "The build pipeline's default branch"
- Save

## Task 3: Configuring the Azure app services for CD
1. Open the SQL Database - get the db connection strings
2. Copy the ADO.NET string to your clipboard.
3. Update username and password in the connection string with SQL credentials
3. Open the QA app service | Application Settings | Connection Strings
```
DefaultConnectionString: <paste in the connectionstring>
```
4. Click Save
5. Repeat for Prod web app

## Task 4: Invoking a CD release to QA
1. Open Azure Devops Repos tab in a new browser tab
2. Edit ```PartsUnlimited-aspnet45/src/PartsUnlimitedWebsite/Views/Shared/_Layout.cshtml. ```
```
//add v2.0 text after the image
<img src="/images/unlimited_logo.png" >v2.0
```
3. Commit changes
4. Open the build that is kicked off > follow until completion
5. Open the release > follow it until completion
6. Navigate to the QA Site > <app-service-name>.azurewebsites.net
7. Check that it now says 'v2.0' after the image

## Task5: Creating a gated release to the production stage
We are including both automated quality gates as well as a manual approver gate. 
We will make it our policy that the QA deployment cannot be considered a success until all critical bugs have been resolved.

1. Open the Release pipeline. Clone the QA stage. 
2. Apply post-deployment considitions on QA gate
   - Enable the Gates option
   - Change 'Delay before evaluation' to 0
   - Add 'Query Work Items' Deployment gates
   - Query > Shared Queries | Critical Bugs
   - Evuation options > Time between re-evaluation of gates to 5.
3. Rename 'Copy of QA' to Prod
4. Add Pre-deployment approvals > add yourself as an Approver
5. Click the Prod job > change the app service name to be the Prod web app
6. Save the pipeline
   
