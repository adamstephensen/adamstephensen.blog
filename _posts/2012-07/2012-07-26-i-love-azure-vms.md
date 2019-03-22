---
title: I love Azure VMs
permalink: /2012/07/26/i-love-azure-vms/
layout: post
tags:
  - Azure
comments: true
---

Microsoft has released the ability to easily create a Virtual Machine hosted on Azure

<a href="./images/image005.png"><img class="alignnone size-medium wp-image-150" title="image005" src="./images/image005.png?w=300" alt="" width="300" height="132" /></a>

Figure: I can’t quite believe how easy it is to ‘Quick Create’ a new Virtual machine. It literally takes a few minutes to have a Windows Server running in the cloud.

<a href="./images/image0071.png"><img class="alignnone size-medium wp-image-151" title="image0071" src="./images/image0071.png?w=300" alt="" width="300" height="217" /></a>

Figure: Alternatively you create a Windows or LINUX VM from selection of images in the Gallery. You can also add your own images to the gallery. This process only takes marginally longer than Quick Create, but gives you more options for customization.
<h3>Situations where I love Azure VMs</h3>
<strong>1. Have a Dev box in the cloud</strong>

I have an Azure VM with Visual Studio 2012 and SQL Express 2012 on it.

I keep it at an Extra-Small instance for most of the month ($15/month) and ramp it up to a Large/Extra Large instance when I want to work on it.

<a href="./images/image0041.png"><img class="alignnone size-medium wp-image-147" title="image0041" src="./images/image0041.png?w=300" alt="" width="300" height="142" /></a>

Figure: Changing the size of the VM is amazingly simple. Log onto the portal, choose an option from the drop down and click Save. Wait a few minutes and log back in.

<a href="./images/image006.jpg"><img class="alignnone size-medium wp-image-148" title="image006" src="./images/image006.jpg?w=300" alt="" width="300" height="225" /></a>

Figure: I love that I can connect to my Dev VM from anywhere…. Including my iPad

<a href="./images/image008.jpg"><img class="alignnone size-medium wp-image-149" title="image008" src="./images/image008.jpg?w=300" alt="" width="300" height="225" /></a>

Figure: Running Visual Studio 2012 on Azure from the iPad (the Apple Wireless keyboard <em>nearly</em> makes this workable)

Would I pay $233 per month to leave it as a large instance and make this my full time dev environment - No.

<strong>2. Training machines in the cloud.</strong>

Similar to the above situation, it was great to be able to spin up 24 Medium instances to have people do labs on at the Enterprise MVC course.

Attendees were given RPD credentials and logged into their own Azure VM.

The alternatives we considered were

- Each attendee downloads and installs Visual Studio 2012 RC and SQL Express 2012 on their laptops

- Each attendee brings a laptop running a 64 bit OS capable of running a VM, and downloads a VM onto their machine.

The issues that we had with using Azure VMs to run training machines were

- Medium VMs were a bit slow – next time we should use Large

- RPD is not heavy, but we did have issues in some offices with the number of people connected to the available wireless routers

- The network connection died at one training venue. Luckily this happened late in the afternoon when most people had completed the lab exercises

- Some VMs would simply fail to provision. The VM feature is not actually released yet and I’m sure this will be addressed

- Provisioning the machines takes some time because they have to be done synchronously. i.e. Create a new VM, wait for it to finish provisioning and then create the next one.
This is something we will look at automating ourselves, but it would be great to have the functionality available on the MS portal.

For a single day of training with 24 Medium VMs this cost about $50. This is incredible value.
<h3>Situations where I do not think Azure VMs are the answer</h3>
<strong>1. Hosted Full Time Server</strong>

For a full time machine of reasonable size you are looking at $335 or $671 per month. I doubt this is cost effective.

I’d be interested to hear from some Sys Admin types about what they believe their on-premise servers cost them per month.
<h3>Azure VM Pricing Summary</h3>
<table width="418" border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td><strong>Preview Prices</strong></td>
<td valign="bottom">cores</td>
<td valign="bottom">memory</td>
<td valign="bottom">per hr</td>
<td valign="bottom">per day</td>
<td valign="bottom">per month</td>
</tr>
<tr>
<td>Extra Small</td>
<td>Shared</td>
<td>768Mb</td>
<td>$ 0.013</td>
<td>$ 0.31</td>
<td>$ 9.49</td>
</tr>
<tr>
<td>Small</td>
<td>1</td>
<td>1.75 GB</td>
<td>$ 0.080</td>
<td>$ 1.92</td>
<td>$ 58.40</td>
</tr>
<tr>
<td>Medium</td>
<td>2</td>
<td>3.5 GB</td>
<td>$ 0.160</td>
<td>$ 3.84</td>
<td>$ 116.80</td>
</tr>
<tr>
<td>Large</td>
<td>4</td>
<td>7 GB</td>
<td>$ 0.320</td>
<td>$ 7.68</td>
<td>$ 233.60</td>
</tr>
<tr>
<td>Extra Large</td>
<td>8</td>
<td>14 GB</td>
<td>$ 0.640</td>
<td>$ 15.36</td>
<td>$ 467.20</td>
</tr>
<tr>
<td colspan="6"><strong>Figure: This is the pricing while the VM feature is in preview</strong></td>
</tr>
<tr>
<td><strong>Release Prices</strong></td>
<td valign="bottom">cores</td>
<td valign="bottom">memory</td>
<td valign="bottom">per hr</td>
<td valign="bottom">per day</td>
<td valign="bottom">per month</td>
</tr>
<tr>
<td>Extra Small</td>
<td>Shared</td>
<td>768Mb</td>
<td>$ 0.020</td>
<td>$ 0.48</td>
<td>$ 14.60</td>
</tr>
<tr>
<td>Small</td>
<td>1</td>
<td>1.75 GB</td>
<td>$ 0.115</td>
<td>$ 2.76</td>
<td>$ 83.95</td>
</tr>
<tr>
<td>Medium</td>
<td>2</td>
<td>3.5 GB</td>
<td>$ 0.230</td>
<td>$ 5.52</td>
<td>$ 167.90</td>
</tr>
<tr>
<td>Large</td>
<td>4</td>
<td>7 GB</td>
<td>$ 0.460</td>
<td>$ 11.04</td>
<td>$ 335.80</td>
</tr>
<tr>
<td>Extra Large</td>
<td>8</td>
<td>14 GB</td>
<td>$ 0.920</td>
<td>$ 22.08</td>
<td>$ 671.60</td>
</tr>
<tr>
<td colspan="6"><strong>Figure: This is the pricing after the VM Feature is released</strong></td>
</tr>
</tbody>
</table>
Reference: <a href="https://www.windowsazure.com/en-us/pricing/details/">https://www.windowsazure.com/en-us/pricing/details/</a>