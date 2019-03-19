---
title: Azure Storage Transactions - Being Frugal
permalink: 2012/04/25/azure-storage-transactions/
layout: post
tags:
  - Azure
comments: true
---

## Temp Bot

<iframe src='https://webchat.botframework.com/embed/rex-dev-bot?s=3SnRLwsoneo.DR_IVOP96j7rN7QaaKb_q9LYgBIMkMoYWuwDVok3mnM'  style='min-width: 400px; width: 100%; min-height: 500px;'></iframe>

##Blog

Azure transactions are CHEAP. You get tens of thousands for just a few cents. What is dangerous though is that it is very easy to have your application generate hundreds of thousands of transactions a day.

Every call to Windows Azure Blobs, Tables and Queues count as 1 transaction. Windows Azure diagnostic logs, performance counters, trace statements and IIS logs are written to Table Storage or Blob Storage.

If you are unaware of this, it can quickly add up and either burn through your free trial account, or even create a large unexpected bill.

Note: Azure Storage Transactions do not count calls to SQL Azure.
<h3>Ensure that Diagnostics are Disabled for your web and worker roles</h3>
Having Diagnostics enabled can contribute 25 transactions per minute, this is 36,000 transactions per day.

To Do: Confirm that this is per Web/Worker Role

<a href="./images/image001.png"><img class="alignnone size-medium wp-image-108" title="image001" src="./images/image001.png?w=232" alt="" width="232" height="76" /></a>

<span style="font-size:xx-small;">Figure: Check the properties of your web and worker role configuration files</span>

<a href="./images/azure-disable-diagnostics.jpg"><img class="alignnone size-full wp-image-112" title="azure-disable-diagnostics" src="./images/azure-disable-diagnostics.jpg" alt="" width="575" height="140" /></a>

Figure: Disable diagnostics for both roles
<h3>Disable IntelliTrace and Profiling</h3>
<a href="./images/azure-publishing-settings.jpg"><img class="alignnone size-full wp-image-113" title="azure-publishing-settings" src="./images/azure-publishing-settings.jpg" alt="" width="600" height="403" /></a>

Figure: When publishing, ensure that IntelliTrace and Profiling are both disabled.
<h3>Robots.txt</h3>
Search bots crawling your site to index it will lead to a lot of transactions. Especially for web ‘applications’ that do not need to be searchable, use Robot.txt to save transactions.

<a href="./images/image004.png"><img class="alignnone size-medium wp-image-111" title="image004" src="./images/image004.png?w=214" alt="" width="214" height="95" /></a>

Figure: Place robots.txt in the root of your site to control search engine indexing
<h3>Continuous Deployment</h3>
When deploying to Azure, the deployment package is loaded into the Storage Account. This will also contribute to the transaction count.

If you have enabled continuous deployment to Azure, you will need to monitor your transaction usage carefully.
<h3>References:</h3>
<a title="http://randypatterson.com/2012/01/why-so-many-azure-storage-transactions/" href="http://randypatterson.com/2012/01/why-so-many-azure-storage-transactions/">http://randypatterson.com/2012/01/why-so-many-azure-storage-transactions/</a>

<a href="http://blogs.msdn.com/b/windowsazurestorage/archive/2010/07/09/understanding-windows-azure-storage-billing-bandwidth-transactions-and-capacity.aspx">http://blogs.msdn.com/b/windowsazurestorage/archive/2010/07/09/understanding-windows-azure-storage-billing-bandwidth-transactions-and-capacity.aspx</a>

<a href="http://serverfault.com/questions/363803/does-windows-azure-hosted-service-use-storage-transactions">http://serverfault.com/questions/363803/does-windows-azure-hosted-service-use-storage-transactions</a>


