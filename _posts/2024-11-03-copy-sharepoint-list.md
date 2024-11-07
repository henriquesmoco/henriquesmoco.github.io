---
layout: post
title:  "Copy SharePoint List to Another Site"
date:   2024-11-03 17:30:00 -0500
categories: SharePoint
---
Follow along to see how to copy a SharePoint list to another site using PowerShell. This is very usefull when you create list workflows following ALM practices to keep list changes in sync between `QA` and `PROD`.

As a good ALM practice, avoid making manual edits to the list in production and only push changes from `QA` to `PROD`. This avoids issues like fields with same name added manually to both lists being considered as two different fields.
If you have to edit a production list, or if a site owner did, use the commands below to update `QA` (consider deleting the `QA` list before syncing).

## Disclaimer
This post is about copying a SharePoint list from `QA` to `Production` for Power Automate ALM purposes. To cover other scenarios, like copying list data or document library files look for other `template` commands in PowerShell PnP cmdlets.

## Copy All Site Lists
This command is good when you have lots of lists to copy and do't want to select one by one. Keep in mind that the command will also copy all document libraries as well, but if there's nothing to update nothing will happen.
You can always edit the XML before applying the template to remove a document library, list or security setting you don't want to copy.

{% capture message1 %}
If the list has unique permissions, those will be copied as well.
{% endcapture %}

{% include message-alert.html content=message1 %}


``` powershell
# Connect to source site and get the template for all lists and document libraries
Connect-PnPOnline -Url https://thepowerdev.sharepoint.com/sites/QA-Test -Interactive
Get-PnPSiteTemplate -Out template.xml -Handlers Lists

# Connect to target site and apply the template
Connect-PnPOnline -Url https://thepowerdev.sharepoint.com/sites/Test -Interactive
Invoke-PnPSiteTemplate -Path template.xml
```


## Copy Selected Lists
To copy just the lists you want, use the `Get-PnPSiteTemplate` with the extra parameter `-ListsToExtract`.

``` powershell
Get-PnPSiteTemplate -Out template.xml -Handlers Lists -ListsToExtract "Sandbox", "Archive"
```


## Other Links
- [Get-PnPSiteTemplate cmdlet](https://pnp.github.io/powershell/cmdlets/Get-PnPSiteTemplate.html)
- [Invoke-PnPSiteTemplate cmdlet](https://pnp.github.io/powershell/cmdlets/Invoke-PnPSiteTemplate.html)