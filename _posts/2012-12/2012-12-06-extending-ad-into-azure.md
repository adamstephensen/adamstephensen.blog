---
title: Summary- Microsoft shares considerations for extending AD into Windows Azure
permalink: 2012/12/06/summary-microsoft-shares-considerations-for-extending-ad-into-windows-azure/
layout: post
tags:
  - Azure
comments: true
---

From:
<a href="http://m.techrepublic.com/blog/datacenter/microsoft-shares-considerations-for-extending-ad-into-windows-azure/5860">http://m.techrepublic.com/blog/datacenter/microsoft-shares-considerations-for-extending-ad-into-windows-azure/5860</a>

The article discusses setting up Azure VMs to run Active Directory, as an alternative to using 'Windows Azure Active Directory'

<strong>Key points in this article</strong>

- "To extend AD services such as directory and authentication to VMs in Azure, an architect can now start to include Domain Controllers (DCs) and Read-only DCs (RODCs) in Azure as part of a design or solution."

- "Microsoft lets you BYON (bring your own network) into Windows Azure, so it's technically feasible to securely connect on-premise, WAN, and private cloud networks with Azure virtual networks."

<strong>Reasons to have a DC or RODS in Azure</strong>

1. Latency: Latency in the AD authentication between on-premise and cloud networks can cause timeout issues (e.g. authentication timeouts) and issues for demanding applications.

2. Resiliency: Having a DC/RODC in Azure ensures the cloud environment continues to function if the connection to the on-premise DCs fail.

3. Cost: "Azure download bandwidth charges are saved by keeping AD-related network traffic such as DNS and LDAP in the cloud. There is no charge for uploads into Azure, so an RODC in Azure, which has no outbound replication channel, will save money compared to having Azure VMs use the Azure virtual network for all AD traffic."

4. You need a stand-alone AD: "A self-contained AD that lives only in your Azure cloud might provide directory and authentication services to elastic clusters or farms of computers that have no need for authentication with an on-premise AD."

<strong>Create an AD site in Windows Azure</strong>

- Azure is really just a huge network of VMs. Configuring AD in Azure is almost the same as hosting AD on VMs on-premise....
"general precautions about ensuring AD recoverability when AD is deployed on VMs apply to VMs in Azure."

- Issues discussed.. dynamically-assigned network addresses, defining subnets

<strong>Provision a DC with the Azure data disk type</strong>

- Important details about provisioning a DC:

o "You must add an additional disk to the Azure VM that will be a DC, before running DCPROMO. This second disk must be of the "data" type, not the "OS" type. The C: drive of every Azure VM is of the "OS disk" type, which has a write cache feature that cannot be disabled. Running a DC with the SYSVOL on an Azure OS disk is not recommended and could cause problems with AD."

o "This means you must not perform a default installation of DCPROMO on an Azure VM, but rather you attach a data disk, then run DCPROMO and locate AD files such as SYSVOL on the data disk, not the C: drive. This link at Microsoft has checklists to add an Azure VM data disk or attach an empty data disk: <a href="http://www.windowsazure.com/en-us/manage/windows/how-to-guides/attach-a-disk/">http://www.windowsazure.com/en-us/manage/windows/how-to-guides/attach-a-disk/</a>"

<strong>Alternative Option: "Windows Azure Active Directory" product</strong>

- "Windows Azure Active Directory" - is a separate product

- It is an alternative to setting up Azure VMs to run AD (what we are talking about in this article)

- It is an outsourced AD that lives completely and only in the cloud.

- It appeals to Microsoft Office 365, Dynamics CRM Online, and Windows InTune customers

<strong>Follow Up Reading</strong>

- Guidelines for Deploying Windows Server Active Directory on Windows Azure Virtual Machines <a href="http://msdn.microsoft.com/en-us/library/windowsazure/jj156090.aspx">http://msdn.microsoft.com/en-us/library/windowsazure/jj156090.aspx</a>

- BYON into the public cloud with Azure Virtual Networks
<a href="http://www.techrepublic.com/blog/datacenter/byon-into-the-public-cloud-with-azure-virtual-networks/5740">http://www.techrepublic.com/blog/datacenter/byon-into-the-public-cloud-with-azure-virtual-networks/5740</a>