---
layout: post
title:  "Create a SharePoint Site Template"
date:   2024-11-01 23:30:00 -0500
categories: SharePoint
---
Site templates are the best way to create SharePoint sites with a consistent look and features. You can define default pages, lists and more.
When a site template is selected, Sharepoint runs the site scripts of that template to customize the site.

The site scripts provide the details for the template such as creating new lists or applying a theme. These script actions are run in the background. When the scripts are complete the page will refresh to display the updated site.

## Limitations
- 300 actions (or 100,000 characters) when the scripts are applied asynchronously
- 100 site scripts and 100 site templates per tenant
- Does not work with themes created in Brand Center or out of the box themes
- Requires tenant admin rights

## Our first site template
Let's create a Communications site template that:
- Has a home page and navigation similar to the Communications template
- Has my organization dark theme
- Has a list called `Sandbox`, with columns `Title` and `Description`

### Part 1 - The Script
We will need this JSON (see the [JSON schema](https://learn.microsoft.com/en-us/sharepoint/dev/declarative-customization/site-design-json-schema)):
``` json
{
  "$schema": "https://developer.microsoft.com/json-schemas/sp/site-design-script-actions.schema.json",
  "actions": [
    {
      "verb": "applyTheme",
      "themeName": "Dark Theme TPD"
    },
    {
      "verb": "createSPList",
      "listName": "Sandbox",
      "templateType": 100,
      "subactions": [
        {
          "verb": "setDescription",
          "description": "List to try things out"
        },
        {
          "verb": "addSPField",
          "fieldType": "Text",
          "displayName": "Description",
          "isRequired": false,
          "addToDefaultView": true,
          "id": "ece81f0e-39e8-4185-ba28-422a878ff650"
        }
      ]
    }
  ],
  "version": 1
}
```

### Part 2 - The preview image
This part is optional but nice to have. Create a preview of your template and save on a SharePoint site that will not be deleted, like Brand Center.
It's recommended the picture have 400x300. I saved mine in `sites/BrandGuide/Site Templates/TPD Dark Theme/tpd-dark-theme-preview.png`.

### Part 3 - The command to make it happen
Connect to the Sharepoint tenant (`yourtenant-admin.sharepoint.com`) and use the following PNP PowerShell command to add the script above and the template in one go.
``` powershell
Get-Content 'c:\scripts\tpd-dark-site-script.json' -Raw | ` 
Add-PnPSiteScript -Title "TPD Dark Theme and Sandbox list" | `
Add-PnPSiteDesign `
  -Title "TPD Dark" `
  -Description "Creates sandbox list and applies standard dark theme" `
  -WebTemplate CommunicationSite `
  -ThumbnailUrl "https://thepowerdev.sharepoint.com/sites/BrandGuide/Site%20Templates/TPD%20Dark%20Theme/tpd-dark-theme-preview.png"
```

Finally, create a new site and select your template.


## Other Links
- [Site Template](https://learn.microsoft.com/en-us/sharepoint/dev/declarative-customization/site-design-overview)
- [Site Theming](https://learn.microsoft.com/en-us/sharepoint/dev/declarative-customization/site-theming/sharepoint-site-theming-overview)
- [Brand Center](https://learn.microsoft.com/en-us/sharepoint/brand-center-overview)
- [PNP PowerShell cmdlets](https://learn.microsoft.com/en-us/sharepoint/dev/declarative-customization/site-design-pnppowershell)

**Note**: the JSON schema documentation page for the site script doesn't seem to have all verbs (actions). Copilot showed me verbs to set the home page and add webparts to a page but I didn't test.