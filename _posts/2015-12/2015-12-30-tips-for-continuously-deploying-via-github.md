---
title: Tips for Continuously Deploying to Azure via GitHub
permalink: 2015/12/30/tips-for-continuously-deploying-to-azure-via-github/
layout: post
tags:
  - Azure
  - .NET
  - DevOps
  - Videos
comments: true
---

Continuously deploying from GitHub to Azure should be easy. In this video I discuss 2 issues I found when deploying an API using ASP.Net 5


{% youtube i06hhOZQkVE %}
<h3>tl;dw</h3>
Here is what I was trying to do:
<ul>
	<li>I had a simple ASP.Net 5 Web API project.
For this demo, I just went file | New and chose the Web API Template for an ASP.Net 5 project</li>
	<li><span style="font-weight:400;">I checked it into GitHub</span></li>
	<li><span style="font-weight:400;">I went into Azure and created an API app (I could do the exact same demo using a  Web App)</span></li>
	<li><span style="font-weight:400;">Then I went in and configured continuous deployment in the Azure portal</span></li>
</ul>
<span style="font-weight:400;">It should have been simple.....</span>

 

<span style="font-weight:400;">There are two issues: </span>

<span style="font-weight:400;">#1: Even the most basic ASP.Net 5 project requires at least a B1 Azure instance size. For Free and Shared instances, there will be insufficient space for the build, even though they give you 1 GB of storage.</span>

 

<span style="font-weight:400;">#2: If you want to successfully deploy an ASP.Net 5 project, even if it doesn’t require the wwwroot folder, you need to include it for Azure to recognise the project as an ASP.Net 5 project that needs to be deployed.</span>

i.e. even for a pure web API project that serves no static content. If you don't have a wwwroot folder the project won't be published to Azure, the repo will just be pulled... then the app won't run. (the project.json webroot setting appears to be ignored)

 

For the Microsoft Team:
<ul>
	<li style="font-weight:400;"><span style="font-weight:400;">#1: I would like to be able to create a simple ASP.Net 5 API or Web project and continuously deploy it to Azure via GitHub.. and have it work on the Free instance size.</span>
<ul>
	<li style="font-weight:400;"><span style="font-weight:400;">I think it is important for developers interested in Azure to have the freedom to experiment without worrying about getting charged</span></li>
	<li style="font-weight:400;"><span style="font-weight:400;">This may involve expanding the size of the free tier on Azure, or maybe it means making some exceptions about what is counted towards the 1 gb of storage…. but we want a frictionless entry to continuous deployment of ASP.Net to Azure</span></li>
</ul>
</li>
	<li style="font-weight:400;"><span style="font-weight:400;">#2 The second thing  I really  want to see  is a few more smarts around how we identify if an application is a .Net app and if it needs to be pulled straight into Azure from GitHub, or wether it needs to be compiled and published. It appears at the moment it is looking for the existence of a wwwroot folder to make the decision. Suggestion: should we be checking for the existence of a project.json or a hosting.json and then checking for the webroot setting to assist in this determination? similar to the <a href="https://github.com/aspnet/Announcements/issues/94" target="_blank">work being done on default logic around the webroot</a><a href="https://github.com/aspnet/Announcements/issues/94"> https://github.com/aspnet/Announcements/issues/94</a></span></li>
</ul>
 

