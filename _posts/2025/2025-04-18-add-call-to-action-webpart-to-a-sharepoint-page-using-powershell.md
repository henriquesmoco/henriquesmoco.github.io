---
layout: post
title:  "Add Call To Action WebPart to a SharePoint Page Using PowerShell"
date:   2025-04-18 22:00:00 -0500
categories: [SharePoint]
---

You want to add a `Call to Action` WebPart to your SharePoint page using PowerShell PNP? Good luck finding which JSON you need to use as there's no documentation, or if there is it's very hard to find (as of the time of writing). Or you could just continue reading :+1:

## JSON Properties
SharePoint WebParts use JSON to define their properties, so if you want to change or create a WebPart you need to know which JSON schema to use.

### Get the JSON properties of any WebPart
You can use the code below to get the JSON for any WebPart in your page, but there's a catch! The JSON returned for the `Call to Action` doesn't have all properties set, and you almost need to be a hacker to find out what's missing :disappointed:.

``` powershell
Connect-PnPOnline -Url https://thepowerdev.sharepoint.com/sites/Test -Interactive
$page = Get-PnPPage My-WebPart-Page
$page.Controls[1].PropertiesJson #The 1 here is the control index in your page
```

### Complete JSON Properties
Below is a complete JSON properties sample for the `Call to Action` WebPart. In the next section we will create an object that matches this schema and then convert it to JSON.  
Note the `focalPosition` property is optional, it is used to set the focal point of the image.

``` json
{
    "image":{
        "itemInfo":{
            "listId":"912c2a76-afd6-4f9d-816f-d8ae43a5a819",
            "uniqueId":"fec03c3e-f371-4a90-9f53-468443d2a900",
            "webId":"059e6f28-5024-42a6-8650-932305a29729",
            "siteId":"9f8b8a5b-a9cd-4281-8648-20e63cbbd389"
        },
        "url":"/sites/Test/SiteAssets/SitePages/My-WebPart-Page/beach-background.jpg",
        "zoomRatio":1,
        "focalPosition":{
            "x":49.134948096885807,
            "y":57.23684210526315
        }
    },
    "button":{
        "label":"My Button Text",
        "linkUrl":"https://www.google.com"
    },
    "overlayText":{
        "text":"Call to Action Text"
    },
    "alignment":"Left",
    "minimumLayoutWidth":10
}
```

## Add the WebPart to the Page
Below is the complete powershell script to add a `Call to Action` with a background picture to a SharePoint page called `My-WebPart-Page`. I omitted the focalPosition for brevity.

``` powershell
#Get the properties of the image named beach-background to use in the ItemInfo node
$file = Get-PnPFolderItem -FolderSiteRelativeUrl "siteAssets/SitePages/My-WebPart-Page" -ItemType File | Where-Object { $_.Name -match "beach-background" }
Get-PnPProperty -ClientObject $file -Property 'SiteId' > $null
Get-PnPProperty -ClientObject $file -Property 'WebId' > $null
Get-PnPProperty -ClientObject $file -Property 'ListId' > $null

#Create the WebPart Properties object
$webpartProperties = @{ `
    image=@{ `
        itemInfo=@{ `
            listId=$file.ListId; `
            uniqueId=$file.uniqueId; `
            webId=$file.WebId; `
            siteId=$file.SiteId `
        }; `
        url=$file.ServerRelativeUrl; `
        zoomRatio=1 `
    }; `
    button=@{ `
        label="My Button Text"; `
        linkUrl="https://www.google.com" `
    }; `
    overlayText=@{ `
        text="Call to Action Text" `
    }; `
    alignment="Left"; `
    minimumLayoutWidth=10 `
}

#Convert the Properties object to JSON
$webpartJson = ConvertTo-Json $webpartProperties

#Add a section first. This is only required if your page only has the Banner
Add-PnPPageSection -Page My-WebPart-Page -SectionTemplate OneColumn

#Add the WebPart to the page. Change section and column properties to place the WebPart where you want
Add-PnPPageWebPart -Page My-WebPart-Page -DefaultWebPartType CallToAction -WebPartProperties $webpartJson -Section 2 -Column 1
```

## Other Links
- [PowerShell PNP GitHub](https://github.com/pnp/powershell)
- [Add-PnPPageWebPart cmdlet](https://pnp.github.io/powershell/cmdlets/Add-PnPPageWebPart.html)
- [Add-PnPPageSection cmdlet](https://pnp.github.io/powershell/cmdlets/Add-PnPPageSection.html)