---
layout: post
title:  "Update your SharePoint Framework Generators"
date:   2025-01-12 03:44:00 -0500
categories: [SharePoint, SharePoint Framework]
---

If you are developing SharePoint WebParts or extensions for a while it comes the time to update your generators.

## What is out of date?
To see what is out of date in your npm environment run:
``` cmd
npm -g outdated
```

The response in my case was:
``` cmd
Package                          Current  Wanted  Latest  Location                                      Depended by
@microsoft/generator-sharepoint   1.18.2  1.11.0  1.11.0  node_modules/@microsoft/generator-sharepoint  global
gulp-cli                           2.3.0   3.0.0   3.0.0  node_modules/gulp-cli                         global
yo                                 5.0.0   5.1.0   5.1.0  node_modules/yo                               global
```

## Updating Yeoman
When you run Yeoman it will tell you there's a new version and what command to run to update it, for me it was:

``` cmd
npm install -g yo
```

## Updating Yeoman Generators
To update Yeoman generators, the easiest way would be to run `yo` without arguments and select the option to update your generators, but notice that the `npm -g outdated` command shows we have version `1.18` and latest is `1.11` which is not right.

To update to latest SharePoint generator, 1.20 currently, run:

``` cmd
npm install @microsoft/generator-sharepoint@latest --global
```