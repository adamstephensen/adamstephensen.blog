---
title: Add Application Insights Exception Handling to MVC 6
permalink: 2015/05/21/add-application-insights-exception-handling-to-mvc-5/
layout: post
tags:
  - .NET
comments: true
---

While everyone is making the move to MVC 6 (and it is pretty awesome), not everything is there yet.

Until it works out of the box, here is an easy way to wire up your MVC 6 project to log all exceptions to Application Insights.
<h2>Create the Application Insights resource via the Azure Portal</h2>
1. Sign in to the <a title="" href="http://portal.azure.com/">Azure portal</a>, and create a new Application Insights resource. Choose ASP.NET as the application type.

<img src="https://acomdpsstorage.blob.core.windows.net/dpsmedia-prod/azure.microsoft.com/en-us/documentation/articles/app-insights-start-monitoring-app-health-usage/20150515052611/01-new-asp.png" alt="Click New, Application Insights" />

A <a title="" href="http://azure.microsoft.com/en-us/documentation/articles/app-insights-resources-roles-access-control/">resource</a> in Azure is an instance of a service. This resource is where telemetry from your app will be analyzed and presented to you.

The choice of application type sets the default content of the resource blades and the properties visible in <a title="" href="http://azure.microsoft.com/en-us/documentation/articles/app-insights-metrics-explorer/">Metrics Explorer</a>.
<h4><a id="_take-a-copy-of-the-instrumentation-key" title="" href="http://azure.microsoft.com/en-us/documentation/articles/app-insights-start-monitoring-app-health-usage/#take-a-copy-of-the-instrumentation-key" name="take-a-copy-of-the-instrumentation-key"></a>2. Take a copy of the Instrumentation Key.</h4>
The key identifies the resource, and you'll install it soon in the SDK to direct data to the resource.

<img src="https://acomdpsstorage.blob.core.windows.net/dpsmedia-prod/azure.microsoft.com/en-us/documentation/articles/app-insights-start-monitoring-app-health-usage/20150515052611/02-props-asp.png" alt="Click Properties, select the key, and press ctrl+C" />
<h2>Create the Exception Filter to log all exceptions</h2>
<a href="./images/2015-05-21_11-32-29.png"><img style="background-image:none;padding-top:0;padding-left:0;display:inline;padding-right:0;border:0;" title="2015-05-21_11-32-29" src="./images/2015-05-21_11-32-29.png" alt="2015-05-21_11-32-29" width="395" height="185" border="0" /></a>

Figure: Add the ApplicationInsights.Web NuGet package

<a href="./images/2015-05-21_11-21-27_01.png"><img style="background-image:none;padding-top:0;padding-left:0;display:inline;padding-right:0;border:0;" title="2015-05-21_11-21-27_01" src="./images/2015-05-21_11-21-27_01.png" alt="2015-05-21_11-21-27_01" width="538" height="429" border="0" /></a>

Figure: Create the Telemetry class to instantiate an instance of the TelemetryClient with your InstrumentationKey & the AiHandleErrorAttribute class that will log exceptions to Application Insights.

<a href="./images/2015-05-21_11-25-18.png"><img style="background-image:none;padding-top:0;padding-left:0;display:inline;padding-right:0;border:0;" title="2015-05-21_11-25-18" src="./images/2015-05-21_11-25-18.png" alt="2015-05-21_11-25-18" width="591" height="408" border="0" /></a>

Figure: Wire up the ExceptionFilterAttribute in Startup.cs

