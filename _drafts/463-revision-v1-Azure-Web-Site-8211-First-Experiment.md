---
id: 468
title: 'Azure Web Site &#8211; First Experiment'
date: 2014-04-18T10:14:22+00:00
author: Greg Woods
layout: revision
guid: http://gregwoods.co.uk/2014/04/463-revision-v1/
permalink: /2014/04/463-revision-v1/
---
OK, I'm very late to the party with Windows Azure. My feeble excuse is that I've no use for it in the day job. Like I said.. feeble. Anyway, I decided I wanted to play with Azure, but desired more than &#8216;Hello World' static web page. My WebDev skills need some serious updating, so I wanted a small application which used a database, and built using cutting edge technologies. After a not very exhaustive search, I decided John Papa's CodeCamper app would be ideal. Unfortunately, several half baked or out of date guides on getting it to run on Azure left me frustrated.  So, after about a dozen clone-modify-publish-delete cycles&#8230; I got it to work. Here are the steps.

## Software pre-requisities

  * VS2013
  * NOTE to self: try it with WebMatrix
  * Git

&nbsp;

## Set up your Azure account

I won't go into details here, but here is what you need to be able to access <pic of https://manage.windowsazure.com>

## Get the code

<span style="line-height: 1.5em;">The source is here: https://github.com/johnpapa/CodeCamper</span> <span style="line-height: 1.5em;">If you have git for windows installed, simply: </span>

<pre> <span style="line-height: 1.5em;">git clone </span><span style="line-height: 1.5em;">https://github.com/johnpapa/CodeCamper.git "C:\development\codecampergwtest"</span></pre>

Note: one my work machine I can clone into &#8216;.' (the current directory), yet at home, it results in a directory not empty message

## Get it running locally

  *  open VS2013 as Administrator (if you don't, some NuGet commands will not work)
  * open NuGet package Manager console
  * You'll see a message &#8220;Some NuGet packages are missing from this solution. Click to restore from your online package sources.&#8221;  &#8211; click &#8220;Restore&#8221;
  * Build solution
  * Run solution &#8211; it should all work, with sample data populated

##  Modify it work with Azure db

In order to see the sample data, we need to enable something called &#8216;Data Migrations', which is part of Entity Framework Code First. However, the NuGet command &#8220;Enable-Migrations&#8221; isn't available with Entity Framework 5.0.0 which is setup by default with this solution So in NuGet package manager <span style="line-height: 1.5em;">Get-Help EntityFramework doesn't work! you may need to update help still doesn't work </span>

<span style="line-height: 1.5em;">Update-Package EntityFramework</span>

<span style="line-height: 1.5em;">(updates from 5.0.0 to 6.1.0 as of today) </span>

<span style="line-height: 1.5em;">Enable-Migrations -StartupProjectName CodeCamper.web -ProjectName CodeCamper.Data -EnableAutomaticMigrations </span>

<span style="line-height: 1.5em;">No Entity Framework provider found for the ADO.NET provider with invariant name &#8216;System.Data.SqlServerCe.4.0&#8242; Looks like I need EF for CE first</span>

## Publish It

In solution explorer, right click &#8220;CodeCamper.web&#8221;, click Publish&#8230; In VS2013, there is an option &#8220;Windows Azure Web Sites&#8221;. Choose it, and log in to your Azure account Create a &#8220;New&#8230;&#8221; website Add a unique site name, choose your locale, and create a new Database server, filling in name and credential fields Go through each page of the wizard NOTE to self: &#8220;Execute code first migrations&#8221; is disabled. Because we haven't run it, the published app will have no data Under the Settings Tab, you will see 2 entries for database. I have no idea why, but it caused me problems. For the second one (&#8220;DefaultConnection&#8221;), uncheck &#8220;Use this connection string at runtime&#8221; WHen finished in the wizard, you'll be taken to a working web site