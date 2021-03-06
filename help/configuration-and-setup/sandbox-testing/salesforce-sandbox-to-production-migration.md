---
unique-page-id: 18874694
description: Salesforce Sandbox to Production Migration - Bizible - Product Documentation
title: Salesforce Sandbox to Production Migration
---

# Salesforce Sandbox to Production Migration {#salesforce-sandbox-to-production-migration}

If you chose to test Bizible in a Salesforce Sandbox environment, please follow these instructions to migrate to Production once you are ready. The following instructions assume that you have already downloaded Bizible's packages into your Sandbox org, performed the necessary testing and are ready to push Bizible to Production.  
  
Please don't hesitate to reach out to your Bizible point of contact with any questions or to walk through this over the phone.

## Step 1: Install Bizible Packages into your Production Salesforce Instance {#step-install-bizible-packages-into-your-production-salesforce-instance}

* Install Bizible's two packages into Production with the "All Users" setting

    * Main package: [bizible.com/sf](https://bizible.com/sf)
    * Dashboard package: [bizible.com/dashboard-mt](https://bizible.com/dashboard-mt)

* For more information about Bizible's relationship with Salesforce, take a look at [this article](/help/configuration-and-setup/bizible-and-salesforce/how-bizible-and-salesforce-interact.md)
* Your license will say trial initially but it will be updated to not expire once it comes through Bizible's system
* A bit of Salesforce configuration is necessary. The specific action items are outlined below in step 3

## Step 2: Change connected user in Bizible app to Production user {#step-change-connected-user-in-bizible-app-to-production-user}

* Log-in to the Bizible application at [apps.bizible.com](http://apps.bizible.com)

    * Ensure you log-in with your original Sandbox login credentials

* Navigate to My Account > Settings > Connections
* Click the pencil icon next to your SFDC connection to re-authorize
* You will be prompted for your credentials, be sure to enter Production login details
* This should switch your account from Sandbox to Production
* Please reach out to your Bizible point of contact at this point to validate that the migration was successful

## Step 3: Salesforce Configuration {#step-salesforce-configuration}

[Page Layouts](/help/configuration-and-setup/bizible-and-salesforce/page-layout-instructions.md)
[Permission Sets](/help/configuration-and-setup/bizible-and-salesforce/bizible-permission-sets.md)  
[Sharing reports](https://help.salesforce.com/articleView?id=analytics_share_folder.htm&type=0)
[Hiding unnecessary report types](/help/configuration-and-setup/bizible-and-salesforce/hiding-unnecessary-report-types.md)
[Custom workflow if applicable](/help/advanced-bizible-features/custom-revenue-amount/using-a-custom-revenue-amount-field.md)
