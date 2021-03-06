---
id: 468
title: 'Azure Web Site - First Experiment'
date: 2014-04-18T10:14:22+00:00

layout: single
guid: http://gregwoods.co.uk/2014/04/463-revision-v1/
permalink: /2014/04/azure-website-experiment-1/
---
OK, I'm very late to the party with Windows Azure. My feeble excuse is that I've no use for it in the day job. Like I said.. feeble. Anyway, I decided I wanted to play with Azure, but desired more than 'Hello World' static web page. My WebDev skills need some serious updating, so I wanted a small application which used a database, and built using cutting edge technologies. After a not very exhaustive search, I decided John Papa's CodeCamper app would be ideal. Unfortunately, several half baked or out of date guides on getting it to run on Azure left me frustrated.  So, after about a dozen clone-modify-publish-delete cycles... I got it to work. Here are my very unpolished notes.

## Software pre-requisities

  * VS2013
  * NOTE to self: try it with WebMatrix
  * Git

&nbsp;

## Set up your Azure account

I won't go into details here, but here is what you need to be able to access <pic of https://manage.windowsazure.com>

## Get the code

The source is here: [https://github.com/johnpapa/CodeCamper](https://github.com/johnpapa/CodeCamper)

If you have git for windows installed, simply:

```sh
git clone https://github.com/johnpapa/CodeCamper.git "C:\development\codecampergwtest"
```

Note: one my work machine I can clone into '.' (the current directory), yet at home, it results in a directory not empty message

## Get it running locally

  *  open VS2013 as Administrator (if you don't, some NuGet commands will not work)
  * open NuGet package Manager console
  * You'll see a message "Some NuGet packages are missing from this solution. Click to restore from your online package sources."  - click "Restore"
  * Build solution
  * Run solution - it should all work, with sample data populated

##  Modify it work with Azure db

In order to see the sample data, we need to enable something called 'Data Migrations', which is part of Entity Framework Code First. However, the NuGet command "Enable-Migrations" isn't available with Entity Framework 5.0.0 which is setup by default with this solution So in NuGet package manager <span style="line-height: 1.5em;">Get-Help EntityFramework doesn't work! you may need to update help still doesn't work </span>

```sh
Update-Package EntityFramework
// (updates from 5.0.0 to 6.1.0 as of today)
Enable-Migrations -StartupProjectName CodeCamper.web -ProjectName CodeCamper.Data -EnableAutomaticMigrations
// No Entity Framework provider found for the ADO.NET provider with invariant name 'System.Data.SqlServerCe.4.0&#8242; Looks like I need EF for CE first
```

## Publish It

In solution explorer, right click "CodeCamper.web", click Publish... 

In VS2013, there is an option "Windows Azure Web Sites". Choose it, and log in to your Azure account 

Create a "New..." website Add a unique site name, choose your locale, and create a new Database server, filling in name and credential fields 

Go through each page of the wizard NOTE to self: "Execute code first migrations" is disabled. Because we haven't run it, the published app will have no data under the Settings Tab, you will see 2 entries for database. I have no idea why, but it caused me problems. For the second one ("DefaultConnection"), uncheck "Use this connection string at runtime" When finished in the wizard, you'll be taken to a working web site.

