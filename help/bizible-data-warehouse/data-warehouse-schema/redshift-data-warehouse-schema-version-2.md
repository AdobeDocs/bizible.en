---
unique-page-id: 18874702
description: Redshift Data Warehouse Schema Version 2 - Bizible - Product Documentation
title: Redshift Data Warehouse Schema Version 2
---

# Redshift Data Warehouse Schema Version 2 {#redshift-data-warehouse-schema-version-2}

Data Warehouse (DW) allow the user to take all of Bizible’s recorded data and slice and dice it anyway they want. This includes hooking up the Data Warehouse to a Business Intelligence (BI) platform like Tableau or Domo and using that data to share with the rest of the org. The advantage of using DW is that it contains much more data than what’s shown in Salesforce, such as costs and more data than what we report in the Marketing ROI Dashboard, such as impressions, sessions, and page views.

Below, learn more about the tables that are part of Bizible’s Data Warehouse schema, as well as the columns that are in each table and what relationships and “joins” are possible between each.

## Biz_Accounts {#biz-accounts}

All CRM Accounts that are imported, along with custom Bizible fields.

<table> 
 <colgroup> 
  <col> 
  <col> 
  <col> 
  <col> 
 </colgroup> 
 <tbody> 
  <tr> 
   <td><strong>Column</strong></td> 
   <td><strong>Type (length)</strong></td> 
   <td><strong>Description</strong></td> 
   <td><strong>Possible Relationships</strong></td> 
  </tr> 
  <tr> 
   <td>Id </td> 
   <td>varchar (40)</td> 
   <td> CRM AccountId</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Created_Date_CRM</td> 
   <td>timestamp</td> 
   <td>The created date of the Account from the CRM</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Modified_Date_CRM</td> 
   <td>timestamp</td> 
   <td>The last modified date of the Account from the CRM</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Name</td> 
   <td>varchar (40)</td> 
   <td>The Account Name, as recorded in the CRM</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Web_Site</td> 
   <td>varchar (100)</td> 
   <td>Website that is entered for the Account, used for Lead2Account mapping</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Engagement_Rating</td> 
   <td>varchar (10)</td> 
   <td>A letter grade (A, B, C, D, N/A) that is generated from Bizible’s Machine Learning model. This will be null if ABM is disabled.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Engagement_Score</td> 
   <td>varchar (10)</td> 
   <td>A numerical score calculated by Bizible’s Machine Learning to generate the Predictive Engagement Score (Engagement_Rating). This will be null if ABM is disabled.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Domain</td> 
   <td>varchar (100)</td> 
   <td>The parsed down version of the website, only storing the domain.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Deleted</td> 
   <td>boolean</td> 
   <td>Whether or not the record is deleted in the CRM.</td> 
   <td><br></td> 
  </tr> 
 </tbody> 
</table>

## Biz_Account_To_Emails {#biz-account-to-emails}

Lead and Contact email addresses that are mapped and known under CRM Accounts. This table will be empty if ABM is disabled.

<table> 
 <colgroup> 
  <col> 
  <col> 
  <col> 
  <col> 
 </colgroup> 
 <tbody> 
  <tr> 
   <td><p><strong><span>Column</span></strong></p></td> 
   <td><p><strong><span>Type (length)</span></strong></p></td> 
   <td><p><strong><span>Description</span></strong></p></td> 
   <td><p><strong><span>Possible Relationships</span></strong></p></td> 
  </tr> 
  <tr> 
   <td><p>Account_Id</p></td> 
   <td><p>varchar (40)</p></td> 
   <td><p>CRM AccountId</p></td> 
   <td><p>Account.Id</p></td> 
  </tr> 
  <tr> 
   <td><p>Email</p></td> 
   <td><p>varchar (100)</p></td> 
   <td><p>Any email address that has been mapped to the Account, whether through Contact relationships or from Lead2Account mapping</p><p><br></p></td> 
   <td><p><br></p></td> 
  </tr> 
 </tbody> 
</table>

## Biz_Attribution_Touchpoints {#biz-attribution-touchpoints}

All touchpoints that are associated with an Opportunity. This table will be empty if Opportunity Touchpoints is disabled.

<table> 
 <colgroup> 
  <col> 
  <col> 
  <col> 
  <col> 
 </colgroup> 
 <tbody> 
  <tr> 
   <td><strong>Column</strong></td> 
   <td><strong>Type (length)</strong></td> 
   <td><strong>Description</strong></td> 
   <td><strong>Possible Relationships</strong></td> 
  </tr> 
  <tr> 
   <td>Id</td> 
   <td>varchar (100)</td> 
   <td>A unique Id for the touchpoint</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>User_Touchpoint_Id</td> 
   <td>varchar (256)</td> 
   <td>A lookup to the Biz_User_Touchpoints table to select columns such as email, campaignmember_id, session_id</td> 
   <td>Biz_User_Touchpoints.Id</td> 
  </tr> 
  <tr> 
   <td>Opportunity_Id</td> 
   <td>varchar (40)</td> 
   <td>A lookup to the Biz_Opportunities table to select columns such as Amount or Close Date</td> 
   <td>Biz_Opportunities.Id</td> 
  </tr> 
  <tr> 
   <td>Contact_Id</td> 
   <td>varchar (40)</td> 
   <td>A lookup to the Biz_Contacts table to select columns such as Created Date</td> 
   <td>Biz_Contacts.Id</td> 
  </tr> 
  <tr> 
   <td>Account_Id</td> 
   <td>varchar (40)</td> 
   <td>A lookup to the Biz_Accounts table to select columns such as Website or Engagement Rating</td> 
   <td>Biz_Accounts.Id</td> 
  </tr> 
  <tr> 
   <td>Touchpoint_Date</td> 
   <td>timestamp</td> 
   <td>The date of the recorded touchpoint, which is the date that the session occurred</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Marketing_Touch_Type</td> 
   <td>varchar (32)</td> 
   <td>Referred to in the CRM as “Touchpoint Type.” This records the type of activity, whether it was a Web Visit, Web Form, Web Chat, Phone Call, [CRM] Campaign, or [CRM] Activity</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Channel</td> 
   <td>varchar (64)</td> 
   <td>Referred to in the CRM as “Marketing Channel - Path.” This is the channel that the touchpoint falls into, as defined in the custom channel definitions within the Bizible App.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Categories</td> 
   <td>varchar (256)</td> 
   <td>Referred to in the CRM as “Segments.” These are the categories and segments that the touchpoint falls into, as defined in the segment definitions within the Bizible App.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Browser_Name</td> 
   <td>varchar (32)</td> 
   <td>From the javascript and IP address, the detected browser that the user was on during the session. For example, Chrome or Internet Explorer.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Browser_Version</td> 
   <td>varchar (20)</td> 
   <td>From the javascript and IP address, the detected version of the browser that the user was on during the session. For example, Chrome or Internet Explorer.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Platform_Name</td> 
   <td>varchar (32)</td> 
   <td>From the javascript and IP address, the detected platform that the user was on during the session. For example, Mac or Windows.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Platform_Version</td> 
   <td>varchar (20)</td> 
   <td>From the javascript and IP address, the detected version of the platform that the user was on during the session. For example, Mac or Windows.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Landing_Page</td> 
   <td>varchar (256)</td> 
   <td>Referred to in the CRM as “Landing Page - Raw.” This is the first landing page of the session that resulted in a touchpoint. A raw landing page will contain all query parameters in the URL.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Referrer_Page</td> 
   <td>varchar (256)</td> 
   <td>Referred to in the CRM as “Referrer Page - Raw.” This is the usually the external landing page immediately before the user comes onto the website. A raw referrer page may contain query parameters in the URL.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Form_Page</td> 
   <td>varchar (256)</td> 
   <td>Referred to in the CRM as “Form - URL.” This is the first form that is recorded in a session that resulted in a touchpoint. Subsequent form submissions will not show up in the Biz_Attribution_Touchpoints table, but rather in the Biz_Form_Submits table.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Form_Date</td> 
   <td>timestamp</td> 
   <td>The date that the form submission occurred.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>City</td> 
   <td>varchar (50)</td> 
   <td>From the javascript and IP address, the detected city that the user was in during the session. For example, Seattle or Vancouver.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Region</td> 
   <td>varchar (50)</td> 
   <td>From the javascript and IP address, the detected city that the user was in during the session. For example, Washington or British Columbia.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Country</td> 
   <td>varchar (50)</td> 
   <td>From the javascript and IP address, the detected city that the user was in during the session. For example, United States or Canada.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Medium</td> 
   <td>varchar (32)</td> 
   <td>Used to define the medium that resulted in the touchpoint. This can either be parsed out from the URL from utm_medium or if Bizible is able to resolve an ad, it may be values such as “cpc” or “display.”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Web_Source</td> 
   <td>varchar (64)</td> 
   <td>Referred to in the CRM as “Touchpoint Source.” Used to define the source that resulted in the touchpoint. This can be parsed out from the URL from utm_source or generically set as “CRM Campaign” if it was synced from the CRM or if Bizible is able to resolve an ad, it may be values such as “Google AdWords” or “Facebook.”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Search_Phrase</td> 
   <td>varchar (200)</td> 
   <td>The value that the user entered in the browser to search for and end up on the website. Depending on the keyword buys, this may or may not match the keywords purchased from the Paid Search platform.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Provider</td> 
   <td>varchar (30)</td> 
   <td>The ad platform that Bizible was able to resolve from, typically one of our integration partners.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Account_Name</td> 
   <td>varchar (32)</td> 
   <td>The name of the ads account in which the ad was resolved from, such as Bizible-US.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Account_Unique_Id</td> 
   <td>varchar (32)</td> 
   <td>The Id of the ads account in which the ad was resolved from.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Advertiser_Name</td> 
   <td>varchar (64)</td> 
   <td>The name of the advertiser from the ads account in which the ad was resolved from, such as Bizible Inc.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Advertiser_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the advertiser from the ads accounts in which the ad was resolved from.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Site_Name</td> 
   <td>varchar (64)</td> 
   <td>The site name from the ads account in which the ad was resolved from, such as Quantcast or TechCrunch. This only applies to Doubleclick Campaign Manager.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Site_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the site from the ads account in which the ad was resolved from. This only applies to Doubleclick Campaign Manager.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Placement_Name</td> 
   <td>varchar (64)</td> 
   <td>The placement name from the ads account in which the ad was resolved from, such as 300x250 or Home Page Takeover. This only applies to Doubleclick Campaign Manager.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Placement_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id placement from the ads account in which the ad was resolved from. This only applies to Doubleclick Campaign Manager.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Campaign_Name</td> 
   <td>varchar (128)</td> 
   <td>The campaign name from the ads account in which the ad was resolved from, such as Winter Promotion 2018 or Planning Your Budget Webinar.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Campaign_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the campaign from the ads account in which the ad was resolved from.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Group_Name</td> 
   <td>varchar (200)</td> 
   <td>The ad group name from the ads account in which the ad was resolved from. This only applies to Google AdWords.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Group_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the ad group from the ads account in which the ad was resolved from. This only applies to Google Adwords.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Name</td> 
   <td>varchar (64)</td> 
   <td>The ad name from the ads account in which the ad was resolved from, such as Winter Promo - Green button or Budget Webinar - sidebar. This applies to Doubleclick Campaign Manager and Facebook (display).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The id of the ad from the ads account in which the ad was resolved from. This applies to Doubleclick Campaign Manager and Facebook (display).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Name</td> 
   <td>varchar (100)</td> 
   <td>The creative name from the ads account in which the ad was resolved from, such as Winter Promo - Green button or Budget Webinar - sidebar. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The id of the creative from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Description_1</td> 
   <td>varchar (100)</td> 
   <td>The first line of the creative from the search ad, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Description_2 </td> 
   <td>varchar (100)</td> 
   <td>The second line of the creative from the search ad, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Destination_URL</td> 
   <td>varchar (200)</td> 
   <td>The landing page that clicks through from the search ad, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Display_URL</td> 
   <td>varchar (200)</td> 
   <td>The friendly URL name that’s shown on the search ad, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Keyword_Name</td> 
   <td>varchar (100)</td> 
   <td>The keyword that was purchased from the Paid Search buy, which is pulled from the ads account in which the ad was resolved from, such as Software Discount or Annual Budget. This applies to Google AdWords and Bing Ads (search)</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Keyword_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the keyword that was purchased from the Paid Search buy, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Keyword_Match_Type</td> 
   <td>varchar (16)</td> 
   <td>The type of match that was found between the search phrase and the purchased keyword, such as “broad” or “exact”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_First_Touch</td> 
   <td>boolean</td> 
   <td>Whether or not this touchpoint is treated as the first touch of the opportunity journey</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Lead_Creation_Touch</td> 
   <td>boolean</td> 
   <td>Whether or not this touchpoint is treated as the lead creation touch of the opportunity journey</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Opp_Creation_Touch</td> 
   <td>boolean</td> 
   <td>This column is blank for Biz_Touchpoints. Please refer to Biz_Attribution_Touchpoints table for this information.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Closed_Touch</td> 
   <td>boolean</td> 
   <td>This column is blank for Biz_Touchpoints. Please refer to Biz_Attribution_Touchpoints table for this information.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Stages_Touched</td> 
   <td>varchar (100)</td> 
   <td>This column is blank for Biz_Touchpoints. Please refer to Biz_Attribution_Touchpoints table for this information.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Form_Submission_Touch</td> 
   <td>boolean</td> 
   <td>Whether or not this touchpoint had a form fill during the session</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Impression_Touch</td> 
   <td>boolean</td> 
   <td>Whether or not this touchpoint is treated as the first impression touch of the opportunity journey</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>First_Click_Percentage</td> 
   <td>real</td> 
   <td>The calculated percentage that gets allocated to this touchpoint because it’s a first touch (See Is_First_Touch)</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Last_Anon_Click_Percentage</td> 
   <td>real</td> 
   <td>The calculated percentage that gets allocated to this touchpoint because it’s a lead creation touch (See Is_Last_Anon_Click_Percentage)</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>U_Shape_Percentage</td> 
   <td>real</td> 
   <td>The calculated percentage that gets allocated to this touchpoint because it’s part of a u-shaped touch (See Is_First_Touch and Is_Lead_Creation_Touch)</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>W_Shape_Percentage</td> 
   <td>real</td> 
   <td>This column is blank for Biz_Touchpoints. Please refer to Biz_Attribution_Touchpoints table for this information.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Full_Path_Percentage</td> 
   <td>real</td> 
   <td>This column is blank for Biz_Touchpoints. Please refer to Biz_Attribution_Touchpoints table for this information.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Custom_Model_Percentage </td> 
   <td>real</td> 
   <td>This column is blank for Biz_Touchpoints. Please refer to Biz_Attribution_Touchpoints table for this information.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Deleted</td> 
   <td>boolean</td> 
   <td>Whether this touchpoint is deleted or not. Used for diagnostics to see if a record was deleted in CRM.</td> 
   <td><br></td> 
  </tr> 
 </tbody> 
</table>

## Biz_Campaign_Members {#biz-campaign-members}

All CRM Campaign Members that are imported, along with custom Bizible fields. This table will be empty if Campaign Sync is disabled.

<table> 
 <colgroup> 
  <col> 
  <col> 
  <col> 
  <col> 
 </colgroup> 
 <tbody> 
  <tr> 
   <td><strong>Column</strong></td> 
   <td><strong>Type (length)</strong></td> 
   <td><strong>Description</strong></td> 
   <td><strong>Possible Relationships</strong></td> 
  </tr> 
  <tr> 
   <td>Id</td> 
   <td>varchar (40)</td> 
   <td>CRM CampaignMember Id</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Created_Date_CRM</td> 
   <td>timestamp</td> 
   <td>The created date of the Campaign Member from the CRM</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Modified_Date_CRM</td> 
   <td>timestamp</td> 
   <td>The last modified date of the Campaign Member from the CRM</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Bizible_Touch_Point_Date</td> 
   <td>timestamp</td> 
   <td>(optional) The date and time that the customer sets to override the campaign date and use this value for the Touchpoint Date instead</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Lead_Id</td> 
   <td>varchar (40)</td> 
   <td>The Id for the related Lead that this Campaign Member is tied to</td> 
   <td>Biz_Leads.Id</td> 
  </tr> 
  <tr> 
   <td>Lead_Email</td> 
   <td>varchar (100)</td> 
   <td>The email for the related Lead that this Campaign Member is tied to</td> 
   <td>Biz_Leads.Email</td> 
  </tr> 
  <tr> 
   <td>Contact_Id</td> 
   <td>varchar (40)</td> 
   <td>The Id for the related Contact that this Campaign Member is tied to</td> 
   <td>Biz_Contacts.Id</td> 
  </tr> 
  <tr> 
   <td>Contact_Email</td> 
   <td>varchar (100)</td> 
   <td>The email for the related Contact that this Campaign Member is tied to</td> 
   <td>Biz_Contacts.Email</td> 
  </tr> 
  <tr> 
   <td>Status</td> 
   <td>varchar (100)</td> 
   <td>The Campaign Member’s status, usually set to Sent or Responded or another custom value. This status is tied to the Campaign_Sync_Type to determine which Campaign Members to create touchpoints for</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Has_Responded</td> 
   <td>boolean</td> 
   <td>A true/false value that tells if the Campaign Member was marked as “Responded” from the Status picker</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>First_Responded_Date</td> 
   <td>timestamp</td> 
   <td>A date field that is automatically populated if Has_Responded is marked as true</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Campaign_Name</td> 
   <td>varchar (128)</td> 
   <td>The name for the related Campaign that this Campaign Member is apart of</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Campaign_Id</td> 
   <td>varchar (50)</td> 
   <td>The Id for the related Campaign that this Campaign Member is apart of</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Campaign_Type</td> 
   <td>varchar (64)</td> 
   <td>The Type that’s selected on the related Campaign that this Campaign Member is apart of. The Type is used to map the Marketing Channel.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Campaign_Sync_Type</td> 
   <td>varchar (64)</td> 
   <td>Used to determine which Campaign Members to create touchpoints for. The possible values are: Include All Campaign Members, Include “Responded” Campaign Members, Exclude All Campaign Members</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Lead_Sync_Status</td> 
   <td>varchar (64)</td> 
   <td>Used as an audit field to tell whether or not a touchpoint was generated for this Lead as a Bizible Touchpoint and if not, the reason why it didn’t qualify</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Contact_Sync_Status</td> 
   <td>varchar (64)</td> 
   <td>Used as an audit field to tell whether or not a touchpoint was generated for this Contact as a Bizible Touchpoint and if not, the reason why it didn’t qualify</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Opp_Sync_Status</td> 
   <td>varchar (64)</td> 
   <td>Used as an audit field to tell whether or not a touchpoint was generated for this Contact as a Bizible Attribution Touchpoint and if not, the reason why it didn’t qualify</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Deleted</td> 
   <td>boolean</td> 
   <td>Finds whether or not the Campaign Member that was in the system is deleted. Used for diagnostics to see if a record was deleted in CRM.</td> 
   <td><br></td> 
  </tr> 
 </tbody> 
</table>

## Biz_Chats {#biz-chats}

Chats that have occurred which contain a VisitorId and is related to a Biz_Session. This will contain the email address that was submitted during the chat. This table will be empty if Web Chat is disabled.

<table> 
 <colgroup> 
  <col> 
  <col> 
  <col> 
  <col> 
 </colgroup> 
 <tbody> 
  <tr> 
   <td><strong>Column</strong></td> 
   <td><strong>Type (length)</strong></td> 
   <td><strong>Description</strong></td> 
   <td><strong>Possible Relationships</strong></td> 
  </tr> 
  <tr> 
   <td>Id</td> 
   <td>varchar (128)</td> 
   <td>A unique Id for the chat record</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Session_Id</td> 
   <td>varchar (128)</td> 
   <td>The recorded session Id at the time the chat was logged.</td> 
   <td>Biz_Sessions.Id</td> 
  </tr> 
  <tr> 
   <td>Visitor_Id</td> 
   <td>varchar (100)</td> 
   <td>The first cookie of the related visitor Id</td> 
   <td>Biz_Email_to_Visitor.Id</td> 
  </tr> 
  <tr> 
   <td>Cookie_Id</td> 
   <td>varchar (100)</td> 
   <td>The recorded cookie Id at the time the chat was logged.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Event_Date</td> 
   <td>timestamp</td> 
   <td>The date and time that the chat was logged.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Current_Page</td> 
   <td>varchar (256)</td> 
   <td>The URL of the page where the chat took place.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Email_In_Chat</td> 
   <td>varchar (100)</td> 
   <td>The email address that was provided and captured during the chat</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>IP_Address</td> 
   <td>varchar (40)</td> 
   <td>The recorded IP address at the time the chat was logged</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>City</td> 
   <td>varchar (50)</td> 
   <td>From the javascript and IP address, the detected city that the user was in during the session. For example, Seattle or Vancouver.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Region</td> 
   <td>varchar (50)</td> 
   <td>From the javascript and IP address, the detected city that the user was in during the session. For example, Washington or British Columbia.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Country</td> 
   <td>varchar (50)</td> 
   <td>From the javascript and IP address, the detected city that the user was in during the session. For example, United States or Canada.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>ISP_Name</td> 
   <td>varchar (64)</td> 
   <td>The name of the internet service provider. Populated for customers with advanced Geo IP tracking.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Chat_Source</td> 
   <td>varchar (50)</td> 
   <td>The web source of the web chat.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Deleted</td> 
   <td>boolean</td> 
   <td>Used for diagnostics to see if a record was deleted.</td> 
   <td><br></td> 
  </tr> 
 </tbody> 
</table>

## Biz_Contacts {#biz-contacts}

All CRM Contacts that are imported, along with custom Bizible fields

<table> 
 <colgroup> 
  <col> 
  <col> 
  <col> 
  <col> 
 </colgroup> 
 <tbody> 
  <tr> 
   <td><strong>Column</strong></td> 
   <td><strong>Type (length)</strong></td> 
   <td><strong>Description</strong></td> 
   <td><strong>Possible Relationships</strong></td> 
  </tr> 
  <tr> 
   <td>Id</td> 
   <td>varchar (40)</td> 
   <td>CRM Contact Id</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Created_Date_CRM</td> 
   <td>timestamp</td> 
   <td>The created date of the Contact from the CRM</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Modified_Date_CRM</td> 
   <td>timestamp</td> 
   <td>The last modified date of the Contact from the CRM</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Email</td> 
   <td>varchar (100)</td> 
   <td>The email address of the Contact from the CRM</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Account_Id</td> 
   <td>varchar (50)</td> 
   <td>The Id of the related Account that this Contact is tied to</td> 
   <td>Biz_Accounts.Id</td> 
  </tr> 
  <tr> 
   <td>Lead_Source</td> 
   <td>varchar (64)</td> 
   <td>The source in which the contact was created</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Odds_Of_Conversion</td> 
   <td>real</td> 
   <td>Bizible’s algorithm of estimating whether a contact will help an opportunity close based on the age and stage</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Bizible_Stage</td> 
   <td>varchar (100)</td> 
   <td>The current stage that the Contact is sitting in, recognized as a custom stage that can be created in Bizible’s application.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Bizible_Stage_Previous</td> 
   <td>varchar (100)</td> 
   <td>A string of all stages that the Contact had previously gone through, recognized as custom stages that can be created in Bizible’s application.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Deleted</td> 
   <td>boolean</td> 
   <td>Finds whether or not the Contact that was in the system is deleted</td> 
   <td><br></td> 
  </tr> 
 </tbody> 
</table>

## Biz_Costs {#biz-costs}

All cost data, either from third party integrations or self reported marketing spend, segmented by various dimensions like Account, Channel, Campaign, Creative, Keyword, AdGroup, Site, Placement.

<table> 
 <colgroup> 
  <col> 
  <col> 
  <col> 
  <col> 
 </colgroup> 
 <tbody> 
  <tr> 
   <td><strong>Column</strong></td> 
   <td><strong>Type (length)</strong></td> 
   <td><strong>Description</strong></td> 
   <td><strong>Possible Relationships</strong></td> 
  </tr> 
  <tr> 
   <td>Id</td> 
   <td>varchar (70)</td> 
   <td>A unique Id for the cost record</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Cost_Date</td> 
   <td>timestamp</td> 
   <td>The date that the cost was reported on</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Source</td> 
   <td>varchar (64)</td> 
   <td>The source of the reported cost</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Cost_In_Micro</td> 
   <td>bigint</td> 
   <td>The reported cost of the day in millions. User will need to divide the value by 1000000 before using this column.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Clicks</td> 
   <td>bigint</td> 
   <td>The number of clicks reported for the group for the day</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Impressions</td> 
   <td>bigint</td> 
   <td>The number of impressions reported for the group for the day</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Estimated_Total_Possible_Impressions</td> 
   <td>bigint</td> 
   <td>The total number of impressions that are estimated from DCM for the group for the day</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Deleted</td> 
   <td>boolean</td> 
   <td>Whether or not the record was deleted, used as an audit trail.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Channel_Unique_Id</td> 
   <td>varchar (32)</td> 
   <td>The Id for the marketing channel, created by Bizible</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Channel_Name</td> 
   <td>varchar (64)</td> 
   <td>The name for the marketing channel, created by the customer in the Bizible application</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Channel_Is_Aggregatable_Cost</td> 
   <td>boolean</td> 
   <td>If rolling up costs and summarizing by the channel, filter this column by “TRUE”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Advertiser_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the advertiser pulled from the ads connection</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Advertiser_Name</td> 
   <td>varchar (64)</td> 
   <td>The name of the advertiser pulled from the ads connection</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Advertiser_Is_Aggregatable_Cost</td> 
   <td>boolean</td> 
   <td>If rolling up costs and summarizing by the advertiser, filter this column by “TRUE”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Account_Unique_Id</td> 
   <td>varchar (32)</td> 
   <td>The Id of the ads account pulled from the ads connection</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Account_Name</td> 
   <td>varchar (64)</td> 
   <td>The name of the ads account pulled from the ads connection</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Account_Is_Aggregatable_Cost</td> 
   <td>boolean</td> 
   <td>If rolling up costs and summarizing by the ads account, filter this column by “TRUE”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Campaign_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the campaign pulled from the ads connection</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Campaign_Name</td> 
   <td>varchar (128)</td> 
   <td>The name of the campaign pulled from the ads connection</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Campaign_Is_Aggregatable_Cost</td> 
   <td>boolean</td> 
   <td>If rolling up costs and summarizing by the campaign, filter this column by “TRUE”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Group_Unique_Id</td> 
   <td>varchar (3642)</td> 
   <td>The Id of the ad group pulled from the ads connection</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Group_Name</td> 
   <td>varchar (200)</td> 
   <td>The name of the ad group pulled from the ads connection</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Group_Is_Aggregatable_Cost</td> 
   <td>boolean</td> 
   <td>If rolling up costs and summarizing by the ad group, filter this column by “TRUE”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the ad pulled from the ads connection</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Name</td> 
   <td>varchar (64)</td> 
   <td>The name of the ad pulled from the ads connection</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Is_Aggregatable_Cost</td> 
   <td>boolean</td> 
   <td>If rolling up costs and summarizing by the ad, filter this column by “TRUE”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the creative pulled from the ads connection</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Name</td> 
   <td>varchar (100)</td> 
   <td>The name of the creative pulled from the ads connection</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Is_Aggregatable_Cost</td> 
   <td>boolean</td> 
   <td>If rolling up costs and summarizing by the creative, filter this column by “TRUE”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Keyword_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the keyword pulled from the ads connection</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Keyword_Name</td> 
   <td>varchar (100)</td> 
   <td>The name of the keyword pulled from the ads connection</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Keyword_Is_Aggregatable_Cost</td> 
   <td>boolean</td> 
   <td>If rolling up costs and summarizing by the keyword, filter this column by “TRUE”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Placement_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the placement pulled from the ads connection</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Placement_Name</td> 
   <td>varchar (64)</td> 
   <td>The name of the placement pulled from the ads connection</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Placement_Is_Aggregatable_Cost</td> 
   <td>boolean</td> 
   <td>If rolling up costs and summarizing by the placement, filter this column by “TRUE”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Site_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the site pulled from the ads connection</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Site_Name</td> 
   <td>varchar (64)</td> 
   <td>The name of the site pulled from the ads connection</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Site_Is_Aggregatable_Cost</td> 
   <td>boolean</td> 
   <td>If rolling up costs and summarizing by the site, filter this column by “TRUE”</td> 
   <td><br></td> 
  </tr> 
 </tbody> 
</table>

## Biz_Crm_Events {#biz-crm-events}

All CRM Events that are imported, along with custom Bizible fields.

Requirements: Enable Activities Sync: True

<table> 
 <colgroup> 
  <col> 
  <col> 
  <col> 
  <col> 
 </colgroup> 
 <tbody> 
  <tr> 
   <td><strong>Column</strong></td> 
   <td><strong>Type (length)</strong></td> 
   <td><strong>Description</strong></td> 
   <td><strong>Possible Relationships</strong></td> 
  </tr> 
  <tr> 
   <td>Id</td> 
   <td>varchar (40)</td> 
   <td>CRM Event Id</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Created_Date_CRM</td> 
   <td>timestamp</td> 
   <td>The created date of the Event from the CRM</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Modified_Date_CRM</td> 
   <td>timestamp</td> 
   <td>The last modified date of the Event from the CRM</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Lead_Id</td> 
   <td>varchar (40)</td> 
   <td>The Id of the related Lead that this Event is tied to</td> 
   <td>Biz_Leads.Id</td> 
  </tr> 
  <tr> 
   <td>Lead_Email</td> 
   <td>varchar (100)</td> 
   <td>The email of the related Lead that this Event is tied to</td> 
   <td>Biz_Leads.Email</td> 
  </tr> 
  <tr> 
   <td>Contact_Id</td> 
   <td>varchar (40)</td> 
   <td>The Id of the related Contact that this Event is tied to</td> 
   <td>Biz_Contacts.Id</td> 
  </tr> 
  <tr> 
   <td>Contact_Email</td> 
   <td>varchar (100)</td> 
   <td>The email of the related Contact that this Event is tied to</td> 
   <td>Biz_Contacts.Email</td> 
  </tr> 
  <tr> 
   <td>Bizible_Host_Id</td> 
   <td>varchar (40)</td> 
   <td>Bizible’s CookieId value that is used to populate from an integration partner to map an offline Event to a web session. Requirement: Enable Call Tracking: True</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Event_Start_Date</td> 
   <td>timestamp</td> 
   <td>The start date of the Event record, one of the options used to determine the Bizible Touchpoint Date</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Event_End_Date</td> 
   <td>timestamp</td> 
   <td>The end date of the Event record, one of the options used to determine the Bizible Touchpoint Date</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Deleted</td> 
   <td>boolean</td> 
   <td>Finds whether or not the Task that was in the system is deleted</td> 
   <td><br></td> 
  </tr> 
 </tbody> 
</table>

## Biz_Crm_Tasks {#biz-crm-tasks}

All CRM Tasks that are imported, along with custom Bizible fields.

Requirements: Enable Activities Sync: True OR Enable Call Tracking: True

<table> 
 <colgroup> 
  <col> 
  <col> 
  <col> 
  <col> 
 </colgroup> 
 <tbody> 
  <tr> 
   <td><strong>Column</strong></td> 
   <td><strong>Type (length)</strong></td> 
   <td><strong>Description</strong></td> 
   <td><strong>Possible Relationships</strong></td> 
  </tr> 
  <tr> 
   <td>Id</td> 
   <td>varchar (40)</td> 
   <td>CRM Task Id</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Created_Date_CRM</td> 
   <td>timestamp</td> 
   <td>The created date of the Task from the CRM</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Modified_Date_CRM</td> 
   <td>timestamp</td> 
   <td>The last modified date of the Task from the CRM</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Lead_Id</td> 
   <td>varchar (40)</td> 
   <td>The Id of the related Lead that this Task is tied to</td> 
   <td>Biz_Leads.Id</td> 
  </tr> 
  <tr> 
   <td>Lead_Email</td> 
   <td>varchar (100)</td> 
   <td>The email of the related Lead that this Task is tied to</td> 
   <td>Biz_Leads.Email</td> 
  </tr> 
  <tr> 
   <td>Contact_Id</td> 
   <td>varchar (40)</td> 
   <td>The Id of the related Contact that this Task is tied to</td> 
   <td>Biz_Contacts.Id</td> 
  </tr> 
  <tr> 
   <td>Contact_Email</td> 
   <td>varchar (100)</td> 
   <td>The email of the related Contact that this Task is tied to</td> 
   <td>Biz_Contacts.Email</td> 
  </tr> 
  <tr> 
   <td>Bizible_Host_Id</td> 
   <td>varchar (40)</td> 
   <td>Bizible’s CookieId value that is used to populate from an integration partner to map an offline Task to a web session. Requirement: Enable Call Tracking: True</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Activity_Type</td> 
   <td>varchar (40)</td> 
   <td>Used to describe the type of Task, usually along the lines of Call or Email or any other custom value. For Activities, this value is used to populate the Touchpoint Type and Medium.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Activity_Date</td> 
   <td>timestamp</td> 
   <td>The date that the Task occurred, one of the options used to determine the Bizible Touchpoint Date</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Deleted</td> 
   <td>boolean</td> 
   <td>Finds whether or not the Task that was in the system is deleted</td> 
   <td><br></td> 
  </tr> 
 </tbody> 
</table>

## Biz_Customer_AB_Tests {#biz-customer-ab-tests}

AB Tests that have been recorded which contain a VisitorId and is related to a Biz_Session. This will contain the experiment and variation that the user was shown.

Requirement: Enable AB Tests: Yes

<table> 
 <colgroup> 
  <col> 
  <col> 
  <col> 
  <col> 
 </colgroup> 
 <tbody> 
  <tr> 
   <td><strong>Column</strong></td> 
   <td><strong>Type (length)</strong></td> 
   <td><strong>Description</strong></td> 
   <td><strong>Possible Relationships</strong></td> 
  </tr> 
  <tr> 
   <td>Id</td> 
   <td>varchar (128)</td> 
   <td>A unique Id for the AB test record</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Session_Id</td> 
   <td>varchar (128)</td> 
   <td>The recorded session Id at the time the chat was logged.</td> 
   <td>Biz_Sessions.Id</td> 
  </tr> 
  <tr> 
   <td>Visitor_Id</td> 
   <td>varchar (100)</td> 
   <td>The first cookie of the related visitor Id</td> 
   <td>Biz_Email_to_Visitor.Id</td> 
  </tr> 
  <tr> 
   <td>Cookie_Id</td> 
   <td>varchar (100)</td> 
   <td>The recorded cookie Id at the time the chat was logged.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Event_Date</td> 
   <td>timestamp</td> 
   <td>The date and time that the chat was logged.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Experiment_Id</td> 
   <td>varchar (30)</td> 
   <td>The Id of the experiment that’s pulled from the AB test platform.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Experiment_Name</td> 
   <td>varchar (64)</td> 
   <td>The name of the experiment that’s pulled from the AB test platform.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Variation_Id</td> 
   <td>varchar (30)</td> 
   <td>The Id of the experiment’s variation that’s pulled from the AB test platform.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Variation_Name</td> 
   <td>varchar (64)</td> 
   <td>The name of the experiment’s variation that’s pulled from the AB test platform.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>ABTest_User_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the user that was served the experiment that’s pulled from the AB test platform.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>IP_Address</td> 
   <td>varchar (40)</td> 
   <td>The recorded IP address at the time the experiment was logged.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Deleted</td> 
   <td>boolean</td> 
   <td>Whether or not the record was deleted, used for diagnostics and auditing.</td> 
   <td><br></td> 
  </tr> 
 </tbody> 
</table>

[Back to top](#top)

## Biz_Customer_Events {#biz-customer-events}

Web events that have been recorded using custom events in the Javascript which contain a VisitorId and is related to a Biz_Session.

Requirement: Enable Bizible Events: True 

<table> 
 <colgroup> 
  <col> 
  <col> 
  <col> 
  <col> 
 </colgroup> 
 <tbody> 
  <tr> 
   <td><strong>Column</strong></td> 
   <td><strong>Type (length)</strong></td> 
   <td><strong>Description</strong></td> 
   <td><strong>Possible Relationships</strong></td> 
  </tr> 
  <tr> 
   <td>Id</td> 
   <td>varchar (128)</td> 
   <td>A unique Id for the custom event</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Session_Id</td> 
   <td>varchar (128)</td> 
   <td>The recorded session Id at the time the event was triggered from the javascript.</td> 
   <td>Biz_Sessions.Id</td> 
  </tr> 
  <tr> 
   <td>Visitor_Id</td> 
   <td>varchar (100)</td> 
   <td>The first cookie of the related visitor Id</td> 
   <td>Biz_Email_to_Visitor.Id</td> 
  </tr> 
  <tr> 
   <td>Cookie_Id</td> 
   <td>varchar (100)</td> 
   <td>The recorded cookie Id at the time the event was triggered from the javascript.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Event_Date</td> 
   <td>timestamp</td> 
   <td>The date and time that the event was triggered from the custom javascript.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Key</td> 
   <td>varchar (30)</td> 
   <td>The name given to the event that was triggered from the custom javascript. For example, “Video View”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Value</td> 
   <td>varchar (60)</td> 
   <td>A value that’s given from the event that was triggered from the custom javascript. For example, “75% viewed”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>IP_Address</td> 
   <td>varchar (40)</td> 
   <td>The recorded IP address at the time the event was triggered from the custom javascript.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Deleted</td> 
   <td>boolean</td> 
   <td>Whether or not the record was deleted, used for diagnostics and auditing.</td> 
   <td><br></td> 
  </tr> 
 </tbody> 
</table>

## Biz_Email_To_Visitor_Id {#biz-email-to-visitor-id}

Email addresses mapped to the Visitor_Id

<table> 
 <colgroup> 
  <col> 
  <col> 
  <col> 
 </colgroup> 
 <tbody> 
  <tr> 
   <td><strong>Column</strong></td> 
   <td><strong>Description</strong></td> 
   <td><strong>Possible Relationships</strong></td> 
  </tr> 
  <tr> 
   <td>Email</td> 
   <td>A known email address that’s tied to a given visitor Id from a session</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Visitor_Id</td> 
   <td>The first cookie of the related visitor Id</td> 
   <td><p>Biz_Chats.Visitor_Id</p><p>Biz_Customer_Events.Visitor_Id</p><p>Biz_Customer_AB_Tests.Visitor_Id</p><p>Biz_Form_Submits.Visitor_Id</p><p>Biz_Impressions.Visitor_Id</p><p>Biz_Page_Views.Visitor_Id</p><p>Biz_Sessions.Visitor_Id</p></td> 
  </tr> 
 </tbody> 
</table>

## Biz_Impressions {#biz-impressions}

All impressions that have been fired and recorded which contain a VisitorId and is related to the Biz_Touchpoints. This will contain the resolved ads information of the served impression.

Requirements: Enable View Through: True, Doubleclick by Google: True

<table> 
 <colgroup> 
  <col> 
  <col> 
  <col> 
  <col> 
 </colgroup> 
 <tbody> 
  <tr> 
   <td><strong>Column</strong></td> 
   <td><strong>Type (length)</strong></td> 
   <td><strong>Description</strong></td> 
   <td><strong>Possible Relationships</strong></td> 
  </tr> 
  <tr> 
   <td>Id</td> 
   <td>varchar (128)</td> 
   <td>A unique Id for the impression</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Session_Id</td> 
   <td>varchar (128)</td> 
   <td>The recorded session Id at the time of the impression.</td> 
   <td>Biz_Session.Id</td> 
  </tr> 
  <tr> 
   <td>Visitor_Id</td> 
   <td>varchar (100)</td> 
   <td>The first cookie of the related visitor Id</td> 
   <td>Biz_Email_to_Visitor.Id</td> 
  </tr> 
  <tr> 
   <td>Cookie_Id</td> 
   <td>varchar (100)</td> 
   <td>The recorded cookie Id at the time of the impression</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Event_Date</td> 
   <td>timestamp</td> 
   <td>The date and time that the impression was served</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Current_Page</td> 
   <td>varchar (256)</td> 
   <td>The URL where the impression was served</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Referrer_Page</td> 
   <td>varchar (256)</td> 
   <td>Referred to in the CRM as “Referrer Page - Raw.” This is the usually the external landing page immediately before the user comes onto the website. A raw referrer page may contain query parameters in the URL.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Referrer_Name</td> 
   <td>varchar (256)</td> 
   <td>The title of the Referrer Page.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Web_Source</td> 
   <td>varchar (64)</td> 
   <td>Referred to in the CRM as “Touchpoint Source.” Used to define the source that resulted in the touchpoint. This can be parsed out from the URL from utm_source or generically set as “CRM Campaign” if it was synced from the CRM or if Bizible is able to resolve an ad, it may be values such as “Google AdWords” or “Facebook.”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Device</td> 
   <td>varchar (64)</td> 
   <td>The hardware device that was used during this page view, like tablet or mobile. (Intentionally left blank)</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Provider</td> 
   <td>varchar (30)</td> 
   <td>The ad platform that Bizible was able to resolve from, typically one of our integration partners.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Account_Name</td> 
   <td>varchar (32)</td> 
   <td>The name of the ads account in which the ad was resolved from, such as Bizible-US.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Account_Unique_Id</td> 
   <td>varchar (32)</td> 
   <td>The Id of the ads account in which the ad was resolved from.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Advertiser_Name</td> 
   <td>varchar (64)</td> 
   <td>The name of the advertiser from the ads account in which the ad was resolved from, such as Bizible Inc.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Advertiser_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the advertiser from the ads accounts in which the ad was resolved from.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Site_Name</td> 
   <td>varchar (64)</td> 
   <td>The site name from the ads account in which the ad was resolved from, such as Quantcast or TechCrunch. This only applies to Doubleclick Campaign Manager.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Site_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the site from the ads account in which the ad was resolved from. This only applies to Doubleclick Campaign Manager.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Placement_Name</td> 
   <td>varchar (64)</td> 
   <td>The placement name from the ads account in which the ad was resolved from, such as 300x250 or Home Page Takeover. This only applies to Doubleclick Campaign Manager.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Placement_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id placement from the ads account in which the ad was resolved from. This only applies to Doubleclick Campaign Manager.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Campaign_Name</td> 
   <td>varchar (128)</td> 
   <td>The campaign name from the ads account in which the ad was resolved from, such as Winter Promotion 2018 or Planning Your Budget Webinar.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Campaign_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the campaign from the ads account in which the ad was resolved from.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Group_Name</td> 
   <td>varchar (200)</td> 
   <td>The ad group name from the ads account in which the ad was resolved from. This only applies to Google AdWords.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Group_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the ad group from the ads account in which the ad was resolved from. This only applies to Google Adwords.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Name</td> 
   <td>varchar (64)</td> 
   <td>The ad name from the ads account in which the ad was resolved from, such as Winter Promo - Green button or Budget Webinar - sidebar. This applies to Doubleclick Campaign Manager and Facebook (display).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The id of the ad from the ads account in which the ad was resolved from. This applies to Doubleclick Campaign Manager and Facebook (display).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Name</td> 
   <td>varchar (100)</td> 
   <td>The creative name from the ads account in which the ad was resolved from, such as Winter Promo - Green button or Budget Webinar - sidebar. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The id of the creative from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Description_1</td> 
   <td>varchar (100)</td> 
   <td>The first line of the creative from the search ad, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Description_2 </td> 
   <td>varchar (100)</td> 
   <td>The second line of the creative from the search ad, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Destination_URL</td> 
   <td>varchar (200)</td> 
   <td>The landing page that clicks through from the search ad, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Display_URL</td> 
   <td>varchar (200)</td> 
   <td>The friendly URL name that’s shown on the search ad, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Keyword_Name</td> 
   <td>varchar (100)</td> 
   <td>The keyword that was purchased from the Paid Search buy, which is pulled from the ads account in which the ad was resolved from, such as Software Discount or Annual Budget. This applies to Google AdWords and Bing Ads (search)</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Keyword_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the keyword that was purchased from the Paid Search buy, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Keyword_Match_Type</td> 
   <td>varchar (16)</td> 
   <td>The type of match that was found between the search phrase and the purchased keyword, such as “broad” or “exact”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Campaign</td> 
   <td>varchar (100)</td> 
   <td>Referred to in the CRM as “Ad Campaign Name.” Used to define the ad campaign that resulted in the touchpoint. This can either be parsed out from the URL from utm_campaign or if Bizible is able to resolve an ad, it may be values such as “Winter Promotion 2018” or “Quarterly Customer Webinar.”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Medium</td> 
   <td>varchar (32)</td> 
   <td>Used to define the medium that resulted in the touchpoint. This can either be parsed out from the URL from utm_medium or if Bizible is able to resolve an ad, it may be values such as “cpc” or “display.”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Source</td> 
   <td>varchar (64)</td> 
   <td>Referred to in the CRM as “Touchpoint Source.” Used to define the source that resulted in the touchpoint. This can be parsed out from the URL from utm_source or generically set as “CRM Campaign” if it was synced from the CRM or if Bizible is able to resolve an ad, it may be values such as “Google AdWords” or “Facebook.”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Term</td> 
   <td>varchar (128)</td> 
   <td>Referred to in the CRM as “Keyword Text.” Used the define any targeted keyword terms from the ad platform that resulted in the touchpoint. This can be parsed out from the URL from utm_term or if Bizible is able to resolve the ad, it may be values from the user's search such as “marketing analytics” or “analytics vendors.”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Content</td> 
   <td>varchar (128)</td> 
   <td>Referred to in the CRM as “Ad Content.” Used to share more detail about the ad, whether it’s the size or placement location or creative name. This can be parsed out from the URL from utm_content or if Bizible is able to resolve ad ad, it can be the creative description or ad body.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>IP_Address</td> 
   <td>varchar (100)</td> 
   <td>The recorded IP address at the time of the impression</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>City</td> 
   <td>varchar (50)</td> 
   <td>The resolved city from the IP address. For example, Seattle or Vancouver.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Region</td> 
   <td>varchar (50)</td> 
   <td>The resolved region from the IP address. For example, Washington or British Columbia.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Country</td> 
   <td>varchar (50)</td> 
   <td>The resolved country from the IP address. For example, United States or Canada.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>ISP_Name</td> 
   <td>varchar (64)</td> 
   <td>The name of the internet service provider, used by customers with advanced Geo IP tracking.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Deleted</td> 
   <td>boolean</td> 
   <td>Whether or not the record was deleted, used for diagnostics and auditing.</td> 
   <td><br></td> 
  </tr> 
 </tbody> 
</table>

## Biz_Leads {#biz-leads}

All CRM Leads that are imported, along with custom Bizible fields

<table> 
 <colgroup> 
  <col> 
  <col> 
  <col> 
  <col> 
 </colgroup> 
 <tbody> 
  <tr> 
   <td><strong>Column</strong></td> 
   <td><strong>Type (length)</strong></td> 
   <td><strong>Description</strong></td> 
   <td><strong>Possible Relationships</strong></td> 
  </tr> 
  <tr> 
   <td>Id</td> 
   <td>varchar (40)</td> 
   <td>CRM Lead Id</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Created_Date_CRM</td> 
   <td>timestamp</td> 
   <td>The created date of the Lead from the CRM</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Modified_Date_CRM</td> 
   <td>timestamp</td> 
   <td>The last modified date of the Lead from the CRM</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Email</td> 
   <td>varchar (100)</td> 
   <td>The email address of the Lead from the CRM</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Web_Site</td> 
   <td>varchar (256)</td> 
   <td>Website that is entered for the Lead, used for Lead2Account mapping</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Company</td> 
   <td>varchar (64)</td> 
   <td>The company name that is entered for the Lead, used for Lead2Account mapping</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Lead_Source</td> 
   <td>varchar (100)</td> 
   <td>The value of the Lead Source, as entered in the CRM</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Converted</td> 
   <td>boolean</td> 
   <td>Whether or not the Lead has been converted to a Contact</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Converted_Opportunity_Id</td> 
   <td>varchar (40)</td> 
   <td>The Id of the related Opportunity once the Lead has been converted, if applicable</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Converted_Date</td> 
   <td>timestamp</td> 
   <td>The date that the Lead was converted to a Contact, if applicable</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Converted_Contact_Id</td> 
   <td>varchar (40)</td> 
   <td>The Id of the related Contact once the Lead has been converted, if applicable</td> 
   <td><br></td> 
  </tr> 
 </tbody> 
</table>

## Biz_Opportunities {#biz-opportunities}

All CRM Opportunities that are imported, along with custom Bizible fields

<table> 
 <colgroup> 
  <col> 
  <col> 
  <col> 
  <col> 
 </colgroup> 
 <tbody> 
  <tr> 
   <td><strong>Column</strong></td> 
   <td><strong>Type (length)</strong></td> 
   <td><strong>Description</strong></td> 
   <td><strong>Possible Relationships</strong></td> 
  </tr> 
  <tr> 
   <td>Id</td> 
   <td>varchar (40)</td> 
   <td>CRM Opportunity Id</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Created_Date_CRM</td> 
   <td>timestamp</td> 
   <td>The created date of the Opportunity from the CRM</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Modified_Date_CRM</td> 
   <td>timestamp</td> 
   <td>The last modified date of the Opportunity from the CRM</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Account_Id</td> 
   <td>varchar (40)</td> 
   <td>The Id of the related Account that this Opportunity is tied to</td> 
   <td>Biz_Accounts.Id</td> 
  </tr> 
  <tr> 
   <td>Name</td> 
   <td>varchar (200)</td> 
   <td>The name of the Opportunity</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Won</td> 
   <td>boolean</td> 
   <td>Whether or not the Opportunity has been moved to a stage that is considered Won</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Closed</td> 
   <td>boolean</td> 
   <td>Whether or not the Opportunity has been moved to a stage that is considered closed, which can either be Won or Lost</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Close_Date</td> 
   <td>timestamp</td> 
   <td>The anticipated or actual Close Date set on the Opportunity</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Bizible_Custom_Model_Date</td> 
   <td>timestamp</td> 
   <td>A custom close date, if Close_Date is not used in the CRM, set within the Bizible App to determine which custom Close Date field is being used</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Amount</td> 
   <td>real</td> 
   <td>The deal amount that is expected or closed from the Opportunity</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Converted_From_Lead_Id</td> 
   <td>varchar (40)</td> 
   <td>The Id of the related Lead that had converted into this Opportunity</td> 
   <td>Biz_Leads.Id</td> 
  </tr> 
  <tr> 
   <td>Converted_From_Lead_Email</td> 
   <td>varchar (100)</td> 
   <td>The email of the related Lead that had converted into this Opportunity</td> 
   <td>Biz_Leads.Email</td> 
  </tr> 
  <tr> 
   <td>Primary_Contact_Id</td> 
   <td>varchar (40)</td> 
   <td>If Primary Contact Role is used, the Id of the related Contact that is listed as the primary contact role</td> 
   <td>Biz_Contacts.Id</td> 
  </tr> 
  <tr> 
   <td>Primary_Contact_Email</td> 
   <td>varchar (100)</td> 
   <td>If Primary Contact Role is used, the email d of the related Contact that is listed as the primary contact role</td> 
   <td>Biz_Contacts.Email</td> 
  </tr> 
  <tr> 
   <td>Odds_Of_Conversion</td> 
   <td>real</td> 
   <td>Bizible’s algorithm of estimating whether an opportunity will close based on the age and stage</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Bizible_Stage</td> 
   <td>varchar (32)</td> 
   <td>The current stage that the Contact is sitting in, recognized as a custom stage that can be created in Bizible’s application.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Bizible_Stage_Previous</td> 
   <td>varchar (32)</td> 
   <td>A string of all stages that the Contact had previously gone through, recognized as custom stages that can be created in Bizible’s application.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Deleted</td> 
   <td>boolean</td> 
   <td>Finds whether or not the Contact that was in the system is deleted</td> 
   <td><br></td> 
  </tr> 
 </tbody> 
</table>

[Back to top](#top)

## Biz_Page_Views {#biz-page-views}

Page views form web visits with a VisitorId and is related to Biz_Session. Multiple page views can compose of a single session.

<table> 
 <colgroup> 
  <col> 
  <col> 
  <col> 
  <col> 
 </colgroup> 
 <tbody> 
  <tr> 
   <td><strong>Column</strong></td> 
   <td><strong>Type (length)</strong></td> 
   <td><strong>Description</strong></td> 
   <td><strong>Possible Relationships</strong></td> 
  </tr> 
  <tr> 
   <td>Id</td> 
   <td>varchar (100)</td> 
   <td>A unique Id for the page view</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Session_Id</td> 
   <td>varchar (128)</td> 
   <td>The recorded session Id at the time of the page view</td> 
   <td>Biz_Session.Id</td> 
  </tr> 
  <tr> 
   <td>Visitor_Id</td> 
   <td>varchar (100)</td> 
   <td>The first cookie of the related visitor Id</td> 
   <td>Biz_Email_to_Visitor.Id</td> 
  </tr> 
  <tr> 
   <td>Cookie_Id</td> 
   <td>varchar (100)</td> 
   <td>The recorded cookie Id at the time of the page view</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Event_Date</td> 
   <td>timestamp</td> 
   <td>The date and time of the page view</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Page_Title</td> 
   <td>varchar (256)</td> 
   <td>The title of the page view</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Current_Page</td> 
   <td>varchar (384)</td> 
   <td>The URL of the current page view</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Referrer_Page</td> 
   <td>varchar (512)</td> 
   <td>The URL where page view originated from</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Referrer_Name</td> 
   <td>varchar (32)</td> 
   <td>The name of the page where the page view originated from</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Search_Phrase</td> 
   <td>varchar (256)</td> 
   <td>The value that the user entered in the browser to search for and end up on the website. Depending on the keyword buys, this may or may not match the keywords purchased from the Paid Search platform.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Web_Source</td> 
   <td>varchar (64)</td> 
   <td>Referred to in the CRM as “Touchpoint Source.” Used to define the source that resulted in the touchpoint. This can be parsed out from the URL from utm_source or generically set as “CRM Campaign” if it was synced from the CRM or if Bizible is able to resolve an ad, it may be values such as “Google AdWords” or “Facebook.”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Has_Form</td> 
   <td>boolean</td> 
   <td>Whether or not there was a form fill conducted on this page view</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Has_Chat</td> 
   <td>boolean</td> 
   <td>Whether or not there was a web chat conducted on this page view</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Has_Email</td> 
   <td>boolean</td> 
   <td>Whether or not this page view is mapped to and tied to a known email address</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Has_Crm_Activity</td> 
   <td>boolean</td> 
   <td>Whether or not this page view is mapped to and tied to an offline Activity record</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Device</td> 
   <td>varchar (64)</td> 
   <td>The hardware device that was used during this page view, like tablet or mobile. (Intentionally left blank)</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Provider</td> 
   <td>varchar (30)</td> 
   <td>The ad platform that Bizible was able to resolve from, typically one of our integration partners.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Account_Name</td> 
   <td>varchar (64)</td> 
   <td>The name of the ads account in which the ad was resolved from, such as Bizible-US.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Account_Unique_Id</td> 
   <td>varchar (32)</td> 
   <td>The Id of the ads account in which the ad was resolved from.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Advertiser_Name</td> 
   <td>varchar (64)</td> 
   <td>The name of the advertiser from the ads account in which the ad was resolved from, such as Bizible Inc.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Advertiser_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the advertiser from the ads accounts in which the ad was resolved from.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Site_Name</td> 
   <td>varchar (64)</td> 
   <td>The site name from the ads account in which the ad was resolved from, such as Quantcast or TechCrunch. This only applies to Doubleclick Campaign Manager.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Site_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the site from the ads account in which the ad was resolved from. This only applies to Doubleclick Campaign Manager.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Placement_Name</td> 
   <td>varchar (64)</td> 
   <td>The placement name from the ads account in which the ad was resolved from, such as 300x250 or Home Page Takeover. This only applies to Doubleclick Campaign Manager.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Placement_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id placement from the ads account in which the ad was resolved from. This only applies to Doubleclick Campaign Manager.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Campaign_Name</td> 
   <td>varchar (128)</td> 
   <td>The campaign name from the ads account in which the ad was resolved from, such as Winter Promotion 2018 or Planning Your Budget Webinar.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Campaign_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the campaign from the ads account in which the ad was resolved from.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Group_Name</td> 
   <td>varchar (200)</td> 
   <td>The ad group name from the ads account in which the ad was resolved from. This only applies to Google AdWords.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Group_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the ad group from the ads account in which the ad was resolved from. This only applies to Google Adwords.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Name</td> 
   <td>varchar (64)</td> 
   <td>The ad name from the ads account in which the ad was resolved from, such as Winter Promo - Green button or Budget Webinar - sidebar. This applies to Doubleclick Campaign Manager and Facebook (display).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The id of the ad from the ads account in which the ad was resolved from. This applies to Doubleclick Campaign Manager and Facebook (display).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Name</td> 
   <td>varchar (100)</td> 
   <td>The creative name from the ads account in which the ad was resolved from, such as Winter Promo - Green button or Budget Webinar - sidebar. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The id of the creative from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Description_1</td> 
   <td>varchar (100)</td> 
   <td>The first line of the creative from the search ad, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Description_2 </td> 
   <td>varchar (100)</td> 
   <td>The second line of the creative from the search ad, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Destination_URL</td> 
   <td>varchar (200)</td> 
   <td>The landing page that clicks through from the search ad, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Display_URL</td> 
   <td>varchar (200)</td> 
   <td>The friendly URL name that’s shown on the search ad, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Keyword_Name</td> 
   <td>varchar (100)</td> 
   <td>The keyword that was purchased from the Paid Search buy, which is pulled from the ads account in which the ad was resolved from, such as Software Discount or Annual Budget. This applies to Google AdWords and Bing Ads (search)</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Keyword_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the keyword that was purchased from the Paid Search buy, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Keyword_Match_Type</td> 
   <td>varchar (16)</td> 
   <td>The type of match that was found between the search phrase and the purchased keyword, such as “broad” or “exact”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Campaign</td> 
   <td>varchar (100)</td> 
   <td>Referred to in the CRM as “Ad Campaign Name.” Used to define the ad campaign that resulted in the touchpoint. This can either be parsed out from the URL from utm_campaign or if Bizible is able to resolve an ad, it may be values such as “Winter Promotion 2018” or “Quarterly Customer Webinar.”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Medium</td> 
   <td>varchar (32)</td> 
   <td>Used to define the medium that resulted in the touchpoint. This can either be parsed out from the URL from utm_medium or if Bizible is able to resolve an ad, it may be values such as “cpc” or “display.”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Source</td> 
   <td>varchar (64)</td> 
   <td>Referred to in the CRM as “Touchpoint Source.” Used to define the source that resulted in the touchpoint. This can be parsed out from the URL from utm_source or generically set as “CRM Campaign” if it was synced from the CRM or if Bizible is able to resolve an ad, it may be values such as “Google AdWords” or “Facebook.”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Term</td> 
   <td>varchar (128)</td> 
   <td>Referred to in the CRM as “Keyword Text.” Used the define any targeted keyword terms from the ad platform that resulted in the touchpoint. This can be parsed out from the URL from utm_term or if Bizible is able to resolve the ad, it may be values from the user's search such as “marketing analytics” or “analytics vendors.”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Content</td> 
   <td>varchar (128)</td> 
   <td>Referred to in the CRM as “Ad Content.” Used to share more detail about the ad, whether it’s the size or placement location or creative name. This can be parsed out from the URL from utm_content or if Bizible is able to resolve ad ad, it can be the creative description or ad body.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>IP_Address</td> 
   <td>varchar (100)</td> 
   <td>The recorded IP address at the time the form was submitted</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>City</td> 
   <td>varchar (50)</td> 
   <td>The resolved city from the IP address. For example, Seattle or Vancouver.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Region</td> 
   <td>varchar (50)</td> 
   <td>The resolved region from the IP address. For example, Washington or British Columbia.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Country</td> 
   <td>varchar (50)</td> 
   <td>The resolved country from the IP address. For example, United States or Canada.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>ISP_Name</td> 
   <td>varchar (64)</td> 
   <td>The name of the internet service provider, used by customers with advanced Geo IP tracking</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Deleted</td> 
   <td>boolean</td> 
   <td>Whether or not the record was deleted, mainly used for diagnostics and audits.</td> 
   <td><br></td> 
  </tr> 
 </tbody> 
</table>

[Back to top](#top)

## Biz_Sessions {#biz-sessions}

All recorded sessions associated with a VisitorId. Multiple sessions can be associated to a single visitor.

<table> 
 <colgroup> 
  <col> 
  <col> 
  <col> 
  <col> 
 </colgroup> 
 <tbody> 
  <tr> 
   <td><p><strong><span>Column</span></strong></p></td> 
   <td><p><strong><span>Type (length)</span></strong></p></td> 
   <td><p><strong><span>Description</span></strong></p></td> 
   <td><p><strong><span>Possible Relationships</span></strong></p></td> 
  </tr> 
  <tr> 
   <td>Id</td> 
   <td>varchar (100)</td> 
   <td>A unique Id for the session</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Visitor_Id</td> 
   <td>varchar (100)</td> 
   <td>The first cookie of the related visitor Id</td> 
   <td>Biz_Email_to_Visitor.Id</td> 
  </tr> 
  <tr> 
   <td>Session_Date</td> 
   <td>timestamp</td> 
   <td>The date and time of the session</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Modified_Date</td> 
   <td>timestamp</td> 
   <td>The last time the session was modified</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Marketing_Touch_Type</td> 
   <td>varchar (32)</td> 
   <td>Referred to in the CRM as “Touchpoint Type.” This records the type of activity, whether it was a Web Visit, Web Form, Web Chat, Phone Call, [CRM] Campaign, or [CRM] Activity</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Channel</td> 
   <td>varchar (64)</td> 
   <td>Referred to in the CRM as “Marketing Channel - Path.” This is the channel that the touchpoint falls into, as defined in the custom channel definitions within the Bizible App.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Categories</td> 
   <td>varchar (256)</td> 
   <td>Referred to in the CRM as “Segments.” These are the categories and segments that the touchpoint falls into, as defined in the segment definitions within the Bizible App.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Browser_Name</td> 
   <td>varchar (32)</td> 
   <td>From the javascript and IP address, the detected browser that the user was on during the session. For example, Chrome or Internet Explorer.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Browser_Version</td> 
   <td>varchar (20)</td> 
   <td>From the javascript and IP address, the detected version of the browser that the user was on during the session. For example, Chrome or Internet Explorer.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Platform_Name</td> 
   <td>varchar (32)</td> 
   <td>From the javascript and IP address, the detected platform that the user was on during the session. For example, Mac or Windows.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Platform_Version</td> 
   <td>varchar (20)</td> 
   <td>From the javascript and IP address, the detected version of the platform that the user was on during the session. For example, Mac or Windows.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Landing_Page</td> 
   <td>varchar (256)</td> 
   <td>Referred to in the CRM as “Landing Page - Raw.” This is the first landing page of the session that resulted in a touchpoint. A raw landing page will contain all query parameters in the URL.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Referrer_Page</td> 
   <td>varchar (256)</td> 
   <td>Referred to in the CRM as “Referrer Page - Raw.” This is the usually the external landing page immediately before the user comes onto the website. A raw referrer page may contain query parameters in the URL.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Form_Page</td> 
   <td>varchar (256)</td> 
   <td>Referred to in the CRM as “Form - URL.” This is the first form that is recorded in a session that resulted in a touchpoint. Subsequent form submissions will not show up in the Biz_Attribution_Touchpoints table, but rather in the Biz_Form_Submits table.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Form_Date</td> 
   <td>timestamp</td> 
   <td>The date that the form submission occurred.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>City</td> 
   <td>varchar (50)</td> 
   <td>From the javascript and IP address, the detected city that the user was in during the session. For example, Seattle or Vancouver.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Region</td> 
   <td>varchar (50)</td> 
   <td>From the javascript and IP address, the detected city that the user was in during the session. For example, Washington or British Columbia.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Country</td> 
   <td>varchar (50)</td> 
   <td>From the javascript and IP address, the detected city that the user was in during the session. For example, United States or Canada.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Medium</td> 
   <td>varchar (32)</td> 
   <td>Used to define the medium that resulted in the touchpoint. This can either be parsed out from the URL from utm_medium or if Bizible is able to resolve an ad, it may be values such as “cpc” or “display.”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Web_Source</td> 
   <td>varchar (64)</td> 
   <td>Referred to in the CRM as “Touchpoint Source.” Used to define the source that resulted in the touchpoint. This can be parsed out from the URL from utm_source or generically set as “CRM Campaign” if it was synced from the CRM or if Bizible is able to resolve an ad, it may be values such as “Google AdWords” or “Facebook.”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Search_Phrase</td> 
   <td>varchar (256)</td> 
   <td>The value that the user entered in the browser to search for and end up on the website. Depending on the keyword buys, this may or may not match the keywords purchased from the Paid Search platform.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Provider</td> 
   <td>varchar (30)</td> 
   <td>The ad platform that Bizible was able to resolve from, typically one of our integration partners.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Account_Name</td> 
   <td>varchar (32)</td> 
   <td>The name of the ads account in which the ad was resolved from, such as Bizible-US.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Account_Unique_Id</td> 
   <td>varchar (32)</td> 
   <td>The Id of the ads account in which the ad was resolved from.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Advertiser_Name</td> 
   <td>varchar (64)</td> 
   <td>The name of the advertiser from the ads account in which the ad was resolved from, such as Bizible Inc.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Advertiser_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the advertiser from the ads accounts in which the ad was resolved from.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Site_Name</td> 
   <td>varchar (64)</td> 
   <td>The site name from the ads account in which the ad was resolved from, such as Quantcast or TechCrunch. This only applies to Doubleclick Campaign Manager.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Site_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the site from the ads account in which the ad was resolved from. This only applies to Doubleclick Campaign Manager.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Placement_Name</td> 
   <td>varchar (64)</td> 
   <td>The placement name from the ads account in which the ad was resolved from, such as 300x250 or Home Page Takeover. This only applies to Doubleclick Campaign Manager.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Placement_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id placement from the ads account in which the ad was resolved from. This only applies to Doubleclick Campaign Manager.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Campaign_Name</td> 
   <td>varchar (128)</td> 
   <td>The campaign name from the ads account in which the ad was resolved from, such as Winter Promotion 2018 or Planning Your Budget Webinar.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Campaign_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the campaign from the ads account in which the ad was resolved from.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Group_Name</td> 
   <td>varchar (200)</td> 
   <td>The ad group name from the ads account in which the ad was resolved from. This only applies to Google AdWords.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Group_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the ad group from the ads account in which the ad was resolved from. This only applies to Google Adwords.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Name</td> 
   <td>varchar (64)</td> 
   <td>The ad name from the ads account in which the ad was resolved from, such as Winter Promo - Green button or Budget Webinar - sidebar. This applies to Doubleclick Campaign Manager and Facebook (display).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The id of the ad from the ads account in which the ad was resolved from. This applies to Doubleclick Campaign Manager and Facebook (display).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Name</td> 
   <td>varchar (100)</td> 
   <td>The creative name from the ads account in which the ad was resolved from, such as Winter Promo - Green button or Budget Webinar - sidebar. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The id of the creative from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Description_1</td> 
   <td>varchar (100)</td> 
   <td>The first line of the creative from the search ad, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Description_2 </td> 
   <td>varchar (100)</td> 
   <td>The second line of the creative from the search ad, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Destination_URL</td> 
   <td>varchar (200)</td> 
   <td>The landing page that clicks through from the search ad, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Display_URL</td> 
   <td>varchar (200)</td> 
   <td>The friendly URL name that’s shown on the search ad, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Keyword_Name</td> 
   <td>varchar (100)</td> 
   <td>The keyword that was purchased from the Paid Search buy, which is pulled from the ads account in which the ad was resolved from, such as Software Discount or Annual Budget. This applies to Google AdWords and Bing Ads (search)</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Keyword_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the keyword that was purchased from the Paid Search buy, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Keyword_Match_Type</td> 
   <td>varchar (16)</td> 
   <td>The type of match that was found between the search phrase and the purchased keyword, such as “broad” or “exact”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Form_Submission_Touch</td> 
   <td>boolean</td> 
   <td>Whether or not this touchpoint had a form fill during the session</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Impression_Touch</td> 
   <td>boolean</td> 
   <td>Whether or not this touchpoint is treated as the first impression touch of the opportunity journey</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Deleted</td> 
   <td>boolean</td> 
   <td>Did this session merge with another and should be deleted.</td> 
   <td><br></td> 
  </tr> 
 </tbody> 
</table>

## Biz_Touchpoints {#biz-touchpoints}

All touchpoints that are associated with a Lead and/or Contact. This table will be empty if Lead Touchpoints or Contact Touchpoints are disabled.

<table> 
 <colgroup> 
  <col> 
  <col> 
  <col> 
  <col> 
 </colgroup> 
 <tbody> 
  <tr> 
   <td><strong>Column</strong></td> 
   <td><strong>Type (length)</strong></td> 
   <td><strong>Description</strong></td> 
   <td><strong>Possible Relationships</strong></td> 
  </tr> 
  <tr> 
   <td>Id</td> 
   <td>varchar (100)</td> 
   <td>A unique Id for the touchpoint record</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Email</td> 
   <td>varchar (100)</td> 
   <td>The known email address that’s tied to this touchpoint via a Lead or Contact</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>User_Touchpoint_Id</td> 
   <td>varchar (256)</td> 
   <td>A lookup to the Biz_User_Touchpoints table to select columns such as session_id</td> 
   <td>Biz_User_Touchpoints.Id</td> 
  </tr> 
  <tr> 
   <td>Contact_Id</td> 
   <td>varchar (40)</td> 
   <td>A lookup to the Biz_Contacts table to select columns such as Created Date</td> 
   <td>Biz_Contact.Id</td> 
  </tr> 
  <tr> 
   <td>Account_Id</td> 
   <td>varchar (40)</td> 
   <td>A lookup to the Biz_Accounts table to select columns such as Website or Engagement Rating</td> 
   <td>Biz_Account.Id</td> 
  </tr> 
  <tr> 
   <td>Lead_Id</td> 
   <td>varchar (40)</td> 
   <td>A lookup to the Biz_Leads table to select columns such as Created Date</td> 
   <td>Biz_Lead.Id</td> 
  </tr> 
  <tr> 
   <td>Unique_Id_Person</td> 
   <td>varchar (32)</td> 
   <td>The parent person record that relates to a Lead or Contact</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Touchpoint_Date</td> 
   <td>timestamp</td> 
   <td>The date of the recorded touchpoint, which is the date that the session occurred</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Marketing_Touch_Type</td> 
   <td>varchar (32)</td> 
   <td>Referred to in the CRM as “Touchpoint Type.” This records the type of activity, whether it was a Web Visit, Web Form, Web Chat, Phone Call, [CRM] Campaign, or [CRM] Activity</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Channel</td> 
   <td>varchar (64)</td> 
   <td>Referred to in the CRM as “Marketing Channel - Path.” This is the channel that the touchpoint falls into, as defined in the custom channel definitions within the Bizible App.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Categories</td> 
   <td>varchar (256)</td> 
   <td>Referred to in the CRM as “Segments.” These are the categories and segments that the touchpoint falls into, as defined in the segment definitions within the Bizible App.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Lead_Source</td> 
   <td>varchar (64)</td> 
   <td>The value of the Lead Source, as entered in the CRM</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Browser_Name</td> 
   <td>varchar (32)</td> 
   <td>From the javascript and IP address, the detected browser that the user was on during the session. For example, Chrome or Internet Explorer.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Browser_Version</td> 
   <td>varchar (20)</td> 
   <td>From the javascript and IP address, the detected version of the browser that the user was on during the session. For example, Chrome or Internet Explorer.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Platform_Name</td> 
   <td>varchar (32)</td> 
   <td>From the javascript and IP address, the detected platform that the user was on during the session. For example, Mac or Windows.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Platform_Version</td> 
   <td>varchar (20)</td> 
   <td>From the javascript and IP address, the detected version of the platform that the user was on during the session. For example, Mac or Windows.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Landing_Page</td> 
   <td>varchar (256)</td> 
   <td>Referred to in the CRM as “Landing Page - Raw.” This is the first landing page of the session that resulted in a touchpoint. A raw landing page will contain all query parameters in the URL.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Referrer_Page</td> 
   <td>varchar (256)</td> 
   <td>Referred to in the CRM as “Referrer Page - Raw.” This is the usually the external landing page immediately before the user comes onto the website. A raw referrer page may contain query parameters in the URL.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Form_Page</td> 
   <td>varchar (256)</td> 
   <td>Referred to in the CRM as “Form - URL.” This is the first form that is recorded in a session that resulted in a touchpoint. Subsequent form submissions will not show up in the Biz_Attribution_Touchpoints table, but rather in the Biz_Form_Submits table.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Form_Date</td> 
   <td>timestamp</td> 
   <td>The date that the form submission occurred.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>City</td> 
   <td>varchar (50)</td> 
   <td>From the javascript and IP address, the detected city that the user was in during the session. For example, Seattle or Vancouver.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Region</td> 
   <td>varchar (50)</td> 
   <td>From the javascript and IP address, the detected city that the user was in during the session. For example, Washington or British Columbia.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Country</td> 
   <td>varchar (50)</td> 
   <td>From the javascript and IP address, the detected city that the user was in during the session. For example, United States or Canada.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Medium</td> 
   <td>varchar (32)</td> 
   <td>Used to define the medium that resulted in the touchpoint. This can either be parsed out from the URL from utm_medium or if Bizible is able to resolve an ad, it may be values such as “cpc” or “display.”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Web_Source</td> 
   <td>varchar (64)</td> 
   <td>Referred to in the CRM as “Touchpoint Source.” Used to define the source that resulted in the touchpoint. This can be parsed out from the URL from utm_source or generically set as “CRM Campaign” if it was synced from the CRM or if Bizible is able to resolve an ad, it may be values such as “Google AdWords” or “Facebook.”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Search_Phrase</td> 
   <td>varchar (256)</td> 
   <td>The value that the user entered in the browser to search for and end up on the website. Depending on the keyword buys, this may or may not match the keywords purchased from the Paid Search platform.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Provider</td> 
   <td>varchar (30)</td> 
   <td>The ad platform that Bizible was able to resolve from, typically one of our integration partners.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Account_Name</td> 
   <td>varchar (32)</td> 
   <td>The name of the ads account in which the ad was resolved from, such as Bizible-US.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Account_Unique_Id</td> 
   <td>varchar (32)</td> 
   <td>The Id of the ads account in which the ad was resolved from.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Advertiser_Name</td> 
   <td>varchar (64)</td> 
   <td>The name of the advertiser from the ads account in which the ad was resolved from, such as Bizible Inc.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Advertiser_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the advertiser from the ads accounts in which the ad was resolved from.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Site_Name</td> 
   <td>varchar (64)</td> 
   <td>The site name from the ads account in which the ad was resolved from, such as Quantcast or TechCrunch. This only applies to Doubleclick Campaign Manager.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Site_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the site from the ads account in which the ad was resolved from. This only applies to Doubleclick Campaign Manager.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Placement_Name</td> 
   <td>varchar (64)</td> 
   <td>The placement name from the ads account in which the ad was resolved from, such as 300x250 or Home Page Takeover. This only applies to Doubleclick Campaign Manager.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Placement_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id placement from the ads account in which the ad was resolved from. This only applies to Doubleclick Campaign Manager.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Campaign_Name</td> 
   <td>varchar (128)</td> 
   <td>The campaign name from the ads account in which the ad was resolved from, such as Winter Promotion 2018 or Planning Your Budget Webinar.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Campaign_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the campaign from the ads account in which the ad was resolved from.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Group_Name</td> 
   <td>varchar (200)</td> 
   <td>The ad group name from the ads account in which the ad was resolved from. This only applies to Google AdWords.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Group_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the ad group from the ads account in which the ad was resolved from. This only applies to Google Adwords.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Name</td> 
   <td>varchar (64)</td> 
   <td>The ad name from the ads account in which the ad was resolved from, such as Winter Promo - Green button or Budget Webinar - sidebar. This applies to Doubleclick Campaign Manager and Facebook (display).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The id of the ad from the ads account in which the ad was resolved from. This applies to Doubleclick Campaign Manager and Facebook (display).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Name</td> 
   <td>varchar (100)</td> 
   <td>The creative name from the ads account in which the ad was resolved from, such as Winter Promo - Green button or Budget Webinar - sidebar. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The id of the creative from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Description_1</td> 
   <td>varchar (100)</td> 
   <td>The first line of the creative from the search ad, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Description_2 </td> 
   <td>varchar (100)</td> 
   <td>The second line of the creative from the search ad, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Destination_URL</td> 
   <td>varchar (200)</td> 
   <td>The landing page that clicks through from the search ad, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Display_URL</td> 
   <td>varchar (200)</td> 
   <td>The friendly URL name that’s shown on the search ad, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Keyword_Name</td> 
   <td>varchar (100)</td> 
   <td>The keyword that was purchased from the Paid Search buy, which is pulled from the ads account in which the ad was resolved from, such as Software Discount or Annual Budget. This applies to Google AdWords and Bing Ads (search)</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Keyword_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the keyword that was purchased from the Paid Search buy, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Keyword_Match_Type</td> 
   <td>varchar (16)</td> 
   <td>The type of match that was found between the search phrase and the purchased keyword, such as “broad” or “exact”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_First_Touch</td> 
   <td>boolean</td> 
   <td>Whether or not this touchpoint is treated as the first touch of the opportunity journey</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Lead_Creation_Touch</td> 
   <td>boolean</td> 
   <td>Whether or not this touchpoint is treated as the lead creation touch of the opportunity journey</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Opp_Creation_Touch</td> 
   <td>boolean</td> 
   <td>Whether or not this touchpoint is treated as the opportunity creation touch of the opportunity journey. Because this is the lead model, this is expected to be 0.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Closed_Touch</td> 
   <td>boolean</td> 
   <td>Whether or not this touchpoint is treated as the closed touch of the opportunity journey. Because this is the lead model, this is expected to be 0.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Stages_Touched</td> 
   <td>varchar (100)</td> 
   <td>Whether or not this touchpoint caused the stage transition for these stages</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Form_Submission_Touch</td> 
   <td>boolean</td> 
   <td>Whether or not this touchpoint had a form fill during the session</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Impression_Touch</td> 
   <td>boolean</td> 
   <td>Whether or not this touchpoint is treated as the first impression touch of the opportunity journey</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>First_Click_Percentage</td> 
   <td>real</td> 
   <td>The calculated percentage that gets allocated to this touchpoint because it’s a first touch (See Is_First_Touch)</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Last_Anon_Click_Percentage</td> 
   <td>real</td> 
   <td>The calculated percentage that gets allocated to this touchpoint because it’s a lead creation touch (See Is_Last_Anon_Click_Percentage)</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>U_Shape_Percentage</td> 
   <td>real</td> 
   <td>The calculated percentage that gets allocated to this touchpoint because it’s part of a u-shaped touch (See Is_First_Touch and Is_Lead_Creation_Touch)</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>W_Shape_Percentage</td> 
   <td>real</td> 
   <td>The calculated percentage that gets allocated to this touchpoint because it’s part of a w-shaped touch (See Is_First_Touch, Is_Lead_Creation_Touch, and Is_Opp_Creation_Touch). Because this is the lead model, this is expected to be 0.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Full_Path_Percentage</td> 
   <td>Real</td> 
   <td>The calculated percentage that gets allocated to this touchpoint because it’s part of a full path model (See Is_First_Touch, Is_Lead_Creation_Touch, Is_Opp_Creation_Touch, Is_Closed_Touch). Because this is the lead model, this is expected to be 0.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Custom_Model_Percentage</td> 
   <td>real</td> 
   <td>The calculated percentage that gets allocated to this touchpoint because it’s part of a custom model (See Is_First_Touch, Is_Lead_Creation_Touch, Is_Opp_Creation_Touch, Is_Closed_Touch, Stages Touch). Because this is the lead model, this is expected to be 0.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Deleted</td> 
   <td>boolean</td> 
   <td>Whether or not the record was deleted, used for diagnostics and auditing.</td> 
   <td><br></td> 
  </tr> 
 </tbody> 
</table>

[Back to top](#top)

## Biz_User_Touchpoints {#biz-user-touchpoints}

Any touchpoint recorded that can be tied to an email, so it can be a web visit, web form, chat, or offline event. This table only shows touchpoints and does not record attribution.

<table> 
 <colgroup> 
  <col> 
  <col> 
  <col> 
  <col> 
 </colgroup> 
 <tbody> 
  <tr> 
   <td><strong>Column</strong></td> 
   <td><strong>Type (length)</strong></td> 
   <td><strong>Description</strong></td> 
   <td><strong>Possible Relationships</strong></td> 
  </tr> 
  <tr> 
   <td>Id</td> 
   <td>varchar (256)</td> 
   <td>A unique Id for the user touchpoint</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Email</td> 
   <td>varchar (128)</td> 
   <td>The email address that this Touchpoint is created from</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Session_Id</td> 
   <td>varchar (128)</td> 
   <td>The Id of the related Session that this Touchpoint is created from</td> 
   <td>Biz_Sessions.Id</td> 
  </tr> 
  <tr> 
   <td>Campaign_Member_Id</td> 
   <td>varchar (40)</td> 
   <td>The Id of the related Campaign Member that this Touchpoint is created from</td> 
   <td>Biz_Campaign_Member.Id</td> 
  </tr> 
  <tr> 
   <td>Crm_Event_Id</td> 
   <td>varchar (40)</td> 
   <td>The Id of the related Event that this Touchpoint is created from</td> 
   <td>Biz_Crm_Events.Id</td> 
  </tr> 
  <tr> 
   <td>Crm_Task_Id</td> 
   <td>varchar (40)</td> 
   <td>The Id of the related Task that this Touchpoint is created from</td> 
   <td>Biz_Crm_Tasks.Id</td> 
  </tr> 
  <tr> 
   <td>Touchpoint_Date</td> 
   <td>timestamp</td> 
   <td>The date of the recorded touchpoint, which is the date that the session occurred</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Marketing_Touch_Type</td> 
   <td>varchar (32)</td> 
   <td>Referred to in the CRM as “Touchpoint Type.” This records the type of activity, whether it was a Web Visit, Web Form, Web Chat, Phone Call, [CRM] Campaign, or [CRM] Activity</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Channel</td> 
   <td>varchar (64)</td> 
   <td>Referred to in the CRM as “Marketing Channel - Path.” This is the channel that the touchpoint falls into, as defined in the custom channel definitions within the Bizible App.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Browser_Name</td> 
   <td>varchar (32)</td> 
   <td>From the javascript and IP address, the detected browser that the user was on during the session. For example, Chrome or Internet Explorer.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Browser_Version</td> 
   <td>varchar (20)</td> 
   <td>From the javascript and IP address, the detected version of the browser that the user was on during the session. For example, Chrome or Internet Explorer.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Platform_Name</td> 
   <td>varchar (32)</td> 
   <td>From the javascript and IP address, the detected platform that the user was on during the session. For example, Mac or Windows.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Platform_Version</td> 
   <td>varchar (20)</td> 
   <td>From the javascript and IP address, the detected version of the platform that the user was on during the session. For example, Mac or Windows.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Landing_Page</td> 
   <td>varchar (256)</td> 
   <td>Referred to in the CRM as “Landing Page - Raw.” This is the first landing page of the session that resulted in a touchpoint. A raw landing page will contain all query parameters in the URL.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Referrer_Page</td> 
   <td>varchar (256)</td> 
   <td>Referred to in the CRM as “Referrer Page - Raw.” This is the usually the external landing page immediately before the user comes onto the website. A raw referrer page may contain query parameters in the URL.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Form_Page</td> 
   <td>varchar (256)</td> 
   <td>Referred to in the CRM as “Form - URL.” This is the first form that is recorded in a session that resulted in a touchpoint. Subsequent form submissions will not show up in the Biz_Attribution_Touchpoints table, but rather in the Biz_Form_Submits table.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Form_Date</td> 
   <td>timestamp</td> 
   <td>The date that the form submission occurred.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>City</td> 
   <td>varchar (50)</td> 
   <td>From the javascript and IP address, the detected city that the user was in during the session. For example, Seattle or Vancouver.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Region</td> 
   <td>varchar (50)</td> 
   <td>From the javascript and IP address, the detected city that the user was in during the session. For example, Washington or British Columbia.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Country</td> 
   <td>varchar (50)</td> 
   <td>From the javascript and IP address, the detected city that the user was in during the session. For example, United States or Canada.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Medium</td> 
   <td>varchar (32)</td> 
   <td>Used to define the medium that resulted in the touchpoint. This can either be parsed out from the URL from utm_medium or if Bizible is able to resolve an ad, it may be values such as “cpc” or “display.”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Web_Source</td> 
   <td>varchar (64)</td> 
   <td>Referred to in the CRM as “Touchpoint Source.” Used to define the source that resulted in the touchpoint. This can be parsed out from the URL from utm_source or generically set as “CRM Campaign” if it was synced from the CRM or if Bizible is able to resolve an ad, it may be values such as “Google AdWords” or “Facebook.”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Search_Phrase</td> 
   <td>varchar (200)</td> 
   <td>The value that the user entered in the browser to search for and end up on the website. Depending on the keyword buys, this may or may not match the keywords purchased from the Paid Search platform.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Provider</td> 
   <td>varchar (30)</td> 
   <td>The ad platform that Bizible was able to resolve from, typically one of our integration partners.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Account_Name</td> 
   <td>varchar (32)</td> 
   <td>The name of the ads account in which the ad was resolved from, such as Bizible-US.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Account_Unique_Id</td> 
   <td>varchar (32)</td> 
   <td>The Id of the ads account in which the ad was resolved from.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Advertiser_Name</td> 
   <td>varchar (64)</td> 
   <td>The name of the advertiser from the ads account in which the ad was resolved from, such as Bizible Inc.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Advertiser_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the advertiser from the ads accounts in which the ad was resolved from.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Site_Name</td> 
   <td>varchar (64)</td> 
   <td>The site name from the ads account in which the ad was resolved from, such as Quantcast or TechCrunch. This only applies to Doubleclick Campaign Manager.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Site_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the site from the ads account in which the ad was resolved from. This only applies to Doubleclick Campaign Manager.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Placement_Name</td> 
   <td>varchar (64)</td> 
   <td>The placement name from the ads account in which the ad was resolved from, such as 300x250 or Home Page Takeover. This only applies to Doubleclick Campaign Manager.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Placement_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id placement from the ads account in which the ad was resolved from. This only applies to Doubleclick Campaign Manager.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Campaign_Name</td> 
   <td>varchar (128)</td> 
   <td>The campaign name from the ads account in which the ad was resolved from, such as Winter Promotion 2018 or Planning Your Budget Webinar.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Campaign_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the campaign from the ads account in which the ad was resolved from.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Group_Name</td> 
   <td>varchar (200)</td> 
   <td>The ad group name from the ads account in which the ad was resolved from. This only applies to Google AdWords.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Group_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the ad group from the ads account in which the ad was resolved from. This only applies to Google Adwords.</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Name</td> 
   <td>varchar (64)</td> 
   <td>The ad name from the ads account in which the ad was resolved from, such as Winter Promo - Green button or Budget Webinar - sidebar. This applies to Doubleclick Campaign Manager and Facebook (display).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Ad_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The id of the ad from the ads account in which the ad was resolved from. This applies to Doubleclick Campaign Manager and Facebook (display).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Name</td> 
   <td>varchar (100)</td> 
   <td>The creative name from the ads account in which the ad was resolved from, such as Winter Promo - Green button or Budget Webinar - sidebar. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The id of the creative from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Description_1</td> 
   <td>varchar (100)</td> 
   <td>The first line of the creative from the search ad, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Description_2 </td> 
   <td>varchar (100)</td> 
   <td>The second line of the creative from the search ad, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Destination_URL</td> 
   <td>varchar (200)</td> 
   <td>The landing page that clicks through from the search ad, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Creative_Display_URL</td> 
   <td>varchar (200)</td> 
   <td>The friendly URL name that’s shown on the search ad, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search).</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Keyword_Name</td> 
   <td>varchar (100)</td> 
   <td>The keyword that was purchased from the Paid Search buy, which is pulled from the ads account in which the ad was resolved from, such as Software Discount or Annual Budget. This applies to Google AdWords and Bing Ads (search)</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Keyword_Unique_Id</td> 
   <td>varchar (64)</td> 
   <td>The Id of the keyword that was purchased from the Paid Search buy, which is pulled from the ads account in which the ad was resolved from. This applies to Google AdWords and Bing Ads (search</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Keyword_Match_Type</td> 
   <td>varchar (16)</td> 
   <td>The type of match that was found between the search phrase and the purchased keyword, such as “broad” or “exact”</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Form_Submission_Touch</td> 
   <td>boolean</td> 
   <td>Whether or not this touchpoint had a form fill during the session</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Impression_Touch</td> 
   <td>boolean</td> 
   <td>Whether or not this touchpoint is treated as the first impression touch of the opportunity journey</td> 
   <td><br></td> 
  </tr> 
  <tr> 
   <td>Is_Deleted</td> 
   <td>boolean</td> 
   <td>Whether or not the record was deleted, used for diagnostics and auditing.</td> 
   <td><br></td> 
  </tr> 
 </tbody> 
</table>

[Back to top](#top)

## Sample queries {#sample-queries}

_How many Leads had sessions from Paid Search in 1-month?_

select sum(tp.first_click_percentage)

from biz_leads leads

join biz_touchpoints tp

on leads.Id = tp.Lead_Id

join biz_user_touchpoints utp

on tp.User_Touchpoint_Id = utp.Id

where utp.touchpoint_date >= '2017-08-01' and utp.touchpoint_date < '2017-09-01' and utp.Channel like 'Paid Search%'

_How many sessions are there per Opportunity in Custom Model?_

select top 100 opps.Id, count(utp.&#42;)

from biz_opportunities opps

inner join biz_attribution_touchpoints tp

on opps.Id = tp.Opportunity_Id

inner join biz_user_touchpoints utp

on tp.User_Touchpoint_Id = utp.Id

where tp.Custom_Model_Percentage > 0

group by opps.Id

_What is the revenue per channel in Custom model per month?_

select tp.Channel, extract(year from tp.Touchpoint_date) as year, extract(month from tp.Touchpoint_date) as month, sum(opps.Amount &#42; tp.Custom_Model_percentage) as amountWithAttribution

from biz_opportunities opps

join biz_attribution_touchpoints tp

on opps.Id = tp.Opportunity_Id

group by tp.Channel, extract(year from tp.Touchpoint_date), extract(month from tp.Touchpoint_date) order by 1, 2, 3

_How many anonymous sessions by channel?_

select channel, count

from biz_sessions

group by channel

_What is the top landing page for Leads?_

select top 5 landing_page, count

from biz_sessions

group by landing_page

