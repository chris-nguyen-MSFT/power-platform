---
title: "Set up Archive components | MicrosoftDocs"
description: "Learn how to set up the archive components of the CoE Starter Kit"
author: manuelap-msft
manager: devkeydet
ms.service: power-platform
ms.component: pa-admin
ms.topic: conceptual
ms.date: 01/10/2022
ms.subservice: guidance
ms.author: mapichle
ms.reviewer: jimholtz
search.audienceType: 
  - admin
search.app: 
  - D365CE
  - PowerApps
  - Powerplatform
---

# Set up Archive components

This article will help you to setup the Archive components of the Governance solution.

>[!NOTE]
>Although the flows are called **archive** flows, they do not automatically archive apps and flows. Instead, they ask makers to backup and archive their apps and flows.

This set of functionality allows you to detect unused objects and ask makers to either archive or unshare them to keep your tenant tidy.

>[!IMPORTANT]
>This article assumes you have [installed the governance components solution](before-setup-gov.md) and you have your [environment setup](setup.md#create-your-environment), and are logged in with the [correct identity](setup.md#what-identity-should-i-install-the-coe-starter-kit-with).

## Grant makers environment access

If your solution is installed in a Production environment, make sure your environment is not restricted with an [environment security group](limitations.md#security-groups-and-approvals).

If your solution is installed in a Dataverse for Teams environment, you first need to grant makers that are not part of your Microsoft Team access to the environment so they can participate in approval workflows. [Share an app in Teams Environment](faq.md#share-an-app-from-a-dataverse-for-teams-environment) with your [Power Platform Maker group](setup.md#how-will-you-communicate-with-your-admins-makers-and-end-users).

## Configure mandatory environment variables

You will [update these environment variables](faq.md#update-environment-variables) after solution import. Environment variables are used to store application and flow configuration data. This means that you only have to set the value once per environment and it will be used in all necessary flows and apps in that environment.

>[!TIP]
>Learn how to update environment variables for Production and Dataverse for Teams environments: [Update Environment Variables](faq.md#update-environment-variables).

| Name | Description |
|------|---------------|
| Approval Admin | This is separate from the Admin Email env var because you cannot use a distribution list for approvals. This env var holds the individual or shared account as a result who will be charged with approving removal of unused orphaned objects. |
| Cleanup Old Objects App URL | (Optional) Link to the Cleanup Old Objects canvas app included in this solution. If included, communication about old objects which are considered no longer useful will include the link to make cleanup easier. See: [Get App URL – Production Environment](faq.md#get-a-power-apps-url-from-a-production-environment) or [Get App URL – Teams Environment](faq.md#add-apps-to-microsoft-teams) |
| Flow Approvals URL | (Optional) Link to Power Automate's Approval page for your CoE Environment. If included, communication about old objects which are considered no longer useful will include the link to make cleanup easier. To get the URL Browse to flows.microsoft.com for your CoE Environment > Action Items > Approvals. URL should end in **approvals/received** |  

## Exempt environments from the archive process

There are some environments that you may want to exempt from the archive process - this could be dedicated environments that are already well managed. Learn more: [Establishing an environment strategy](/adoption/environment-strategy)

You can exempt environments from the archive process using the Power Platform Admin View app.  

### Production environment

If your solution is installed in a Production Environment, your app will be a model driven app.  

1. Go to [make.powerapps.com](<https://make.powerapps.com>).
1. Go to your CoE environment.
1. Open the **Power Platform Admin View** app.
1. Select Environments > Chose the environment you want to exempt > Set the **Excuse From Archival Flows** field to Yes > **Save**

   ![Exclude an environment from the archive process in a Production environment](media/coe-archive2.png "Exclude an environment from the compliance process in a Production environment")

### Dataverse for Teams environment

1. Open to the Power Apps app in Teams, select **Build**, and select the Team you have installed the CoE Starter Kit solutions in.
1. Select **Center of Excellence - Core for Teams > See All**.
1. Open the **Power Platform Admin View** app.
1. Select Environments > Chose the environment you want to exempt > Set the **Excuse From Archival Flows** field to Yes > **Save**.

   ![Exclude an environment from the archive process in Dataverse for Teams](media/coe-archive1.png "Exclude an environment from the archive process in Dataverse for Teams")

## Turn on flows

**Turn on** these flows which are installed as part of the **Governance components** solution:

- [Admin | Setup | Ignored Archival Requests](governance-components.md#admin--setup---ignored-archival-requests)
- [Admin | Archive and Clean Up v2 (Check Approval)](governance-components.md#admin--archive-and-clean-up-v2-check-approval)
- [Admin | Archive and Clean Up v2 (Clean Up and Delete)](governance-components.md#admin--archive-and-clean-up-v2-clean-up-and-delete)
- [Admin | Archive and Clean Up v2 (Start Approval for Apps)](governance-components.md#admin--archive-and-clean-up-v2-start-approval-for-apps)
- [Admin | Archive and Clean Up v2 (Start Approval for Flows)](governance-components.md#admin--archive-and-clean-up-v2-start-approval-for-flows)
- [Admin | Email Managers Ignored Approvals](governance-components.md#admin--setup---ignored-archival-requests)

## Share apps with makers

The Governance Components solution contains the [**Archival – Cleanup Unused Objects**](governance-components.md#cleanup-old-objects-app) app for makers and admins to manage archive approvals. Share this app with your makers and admins, assigning them the **Power Platform Maker SR** security role.

More information:

- [Share a canvas app in Power Apps](faq.md#share-an-app-from-a-production-environment)
- [Share a canvas app in Microsoft Teams](faq.md#share-an-app-from-a-dataverse-for-teams-environment)

Consider adding this app to the **Maker - Command Center** for makers to easily find and access it.

## All environment variables

Here is the full list of environment variables that impact the compliance process, including environment variables with Default values. You may have to [update environment variables](faq.md#update-environment-variables) after import.

>[!IMPORTANT]
> You don't have to change the values during setup, just when you need to change the value of an environment variable that you configured during import or when you want to change a default value. Re-start all flows after you change environment variables, to make sure the latest value is picked up.

Environment variables are used to store application and flow configuration data with data specific to your organization or environment.

| Name | Description | Default Value |
|------|---------------|------|
| Approval Admin | This is separate from the Admin Email env var because you cannot use a distribution list for approvals. This env var holds the individual or shared account as a result who will be charged with approving removal of unused orphaned objects. | n/a |
| Auto Delete on Archive | Determines whether apps andd flows are deleted when they're approved for deletion in the following flow: Admin \| App Archive and Clean Up - Check Approvals and Archive. Value must be Yes or No.  | Yes |
| Cleanup Old Objects App URL | (Optional) Link to the Cleanup Old Objects canvas app included in this solution. If included, communication about old objects which are considered no longer useful will include the link to make cleanup easier. See: [Get App URL – Production Environment](faq.md#get-a-power-apps-url-from-a-production-environment) or [Get App URL – Teams Environment](faq.md#add-apps-to-microsoft-teams) | n/a |
| Flow Approvals URL | (Optional) Link to Power Automate's Approval page for your CoE Environment. If included, communication about old objects which are considered no longer useful will include the link to make cleanup easier. To get the URL Browse to flows.microsoft.com for your CoE Environment > Action Items > Approvals. URL should end in **approvals/received** |  n/a |
| ProductionEnvironment | Set to No if you have installed the solution for development/test purposes. This will send approvals to the admin email instead of the maker. | Yes |

## It looks like I found a bug with the CoE Starter Kit; where should I go?

To file a bug against the solution, go to [aka.ms/coe-starter-kit-issues](https://aka.ms/coe-starter-kit-issues).

[!INCLUDE[footer-include](../../includes/footer-banner.md)]
