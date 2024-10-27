---
layout: post
title:  "Install and Configure PowerShell PNP"
date:   2024-10-26 21:30:00 -0500
categories: PowerShell
excerpt: This is a quick one page on how to install and configure PowerShell PNP. Since PowerShell 7 is required, I also show how to install it and keep everything up to date.
---
This is a quick one page on how to install and configure PowerShell PNP. Since PowerShell 7 is required, I also show how to install it and keep everything up to date.

## Installation
### Install PowerShell 7
Use [WinGet](https://learn.microsoft.com/en-us/windows/package-manager/winget/) to install PowerShell 7, or download the official MSI package from [this page](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell-on-windows). WinGet is included in latest Windows 10 and any Windows 11.

{% highlight powershell %}
winget install --id Microsoft.PowerShell --source winget
{% endhighlight %}

### Install PowerShell PNP
Use the PowerShell command below to install PowerShell PNP for the current user (no admin rights needed).

{% highlight powershell %}
Install-Module PnP.PowerShell -Scope CurrentUser
{% endhighlight %}

### Configure PowerShell PNP
Create an Entra App Registration. This is required to connect and authorize PowerShell PNP (more information [here](https://pnp.github.io/powershell/articles/registerapplication.html)).  
Even though the App Registration has `AllSites.FullControl` permission, the user can only perform operations if he/she has permission to perform such operations.

{% highlight powershell %}
Register-PnPEntraIDAppForInteractiveLogin -ApplicationName "Powershell PnP" -Tenant YourTenantHere.onmicrosoft.com -Interactive
{% endhighlight %}

The command above will return the created `APP ID`, use it to create an environment variable named `ENTRAID_CLIENT_ID` (more information [here](https://pnp.github.io/powershell/articles/defaultclientid.html)). If you skip this step, every time you connect you will have to use the `-ClientId` parameter.

{% highlight powershell %}
[System.Environment]::SetEnvironmentVariable('ENTRAID_CLIENT_ID', '<ClientId of your App Registration>', [EnvironmentVariableTarget]::User)
{% endhighlight %}

## Update
### Update PowerShell
{% highlight powershell %}
# Check for upddates
winget list --name PowerShell --upgrade-available

# Update
winget upgrade Microsoft.PowerShell
{% endhighlight %}

### Update PowerShell PNP
{% highlight powershell %}
# Update
Update-Module PnP.PowerShell -Scope CurrentUser

# Find which version is installed
Get-InstalledModule PNP.PowerShell
{% endhighlight %}


## Other Links
- [PowerShell PNP GitHub](https://github.com/pnp/powershell)
- [PowerShell GitHub](https://github.com/PowerShell/PowerShell)