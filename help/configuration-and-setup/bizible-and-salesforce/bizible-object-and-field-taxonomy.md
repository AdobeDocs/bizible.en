---
unique-page-id: 18874584
description: Bizible Object and Field Taxonomy - Bizible - Product Documentation
title: Bizible Object and Field Taxonomy
---

# Bizible Object and Field Taxonomy {#bizible-object-and-field-taxonomy}

Below is a flow chart that represents how Bizible's Custom Objects relate to Salesforce Standard Objects.

![](assets/1-2.png)

For the full-sized image, [click here](http://docs.marketo.com/display/biz/assets/bizible-taxonomy.png).  
  
`Definitions of the Bizible fields that live in each object [can be found here](http://docs.marketo.com/x/2gAgAQ).`

## FAQ {#faq}

**What is the logic in the arrows?**

A: Each arrow describes the relationship between an object and the other. For example, you'll see that the Bizible Person populates fields on the standard Salesforce Lead Object. If it's pointing to it, then it means that it's populating the receiving end of the arrow.

Q: What is the Bizible Person?

A: It's a Custom Bizible Object in Salesforce that links Bizible Touchpoints to Leads and Contacts.

Q: What is the Bizible.JS?

A: It's our custom JavaScript that we utilize to track web information that a person has on a specific site.

Q: What is the Marketing ROI Dashboard?

A: It's a custom marketing channels dashboard that lives in the Bizible app. It can be accessed by going to your Bizible tab in Salesforce.
