---
id: 463
title: CodeCamper SPA, VS2013 and Windows Azure Web Sites
date: 2014-04-18T12:05:37+00:00

layout: single
classes: wide
guid: http://gregwoods.co.uk/?p=463
permalink: /?p=463
categories:
  - Programming
---
OK, I'm very late to the party with Windows Azure. My feeble excuse is that I've no use for it in the day job. Like I said.. feeble. Anyway, I decided I wanted to play with Azure, but desired more than 'Hello World' static web page. My WebDev skills need some serious updating, so I wanted a small application which used a database, and built using cutting edge technologies. After a not very exhaustive search, I decided John Papa's CodeCamper app would be ideal. Unfortunately, several half baked or out of date guides on getting it to run on Azure left me frustrated.  So, after about a dozen clone-modify-publish-delete cycles... I got it to work. Here are the steps.

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

Note: one my work machine I can clone into '.' (the current directory), yet at home, it results in a directory not empty message

## Get it running locally

  *  open VS2013 as Administrator (if you don't, some NuGet commands will not work)
  * open NuGet package Manager console
  * You'll see a message "Some NuGet packages are missing from this solution. Click to restore from your online package sources."  - click "Restore"
  * Build solution
  * Run solution - it should all work, with sample data populated
  * NOTE: on my home PC, I updated EF first and it wouldn't run until I installed EF SqlServerCompact. RETEST without the EF upgrade

##  Modify it work with Azure db

In order to see the sample data, we need to enable something called 'Data Migrations', which is part of Entity Framework Code First. However, the NuGet command "Enable-Migrations" isn't available with Entity Framework 5.0.0 which is setup by default with this solution So in NuGet package manager <span style="line-height: 1.5em;">Get-Help EntityFramework doesn't work! you may need to update help still doesn't work </span>

<span style="line-height: 1.5em;">Update-Package EntityFramework</span>

<span style="line-height: 1.5em;">(updates from 5.0.0 to 6.1.0 as of today) </span>

<span style="line-height: 1.5em;">Enable-Migrations -StartupProjectName CodeCamper.web -ProjectName CodeCamper.Data -EnableAutomaticMigrations </span>

<span style="line-height: 1.5em;">No Entity Framework provider found for the ADO.NET provider with invariant name 'System.Data.SqlServerCe.4.0&#8242; Looks like I need EF for CE first</span>

Using the NuGet GUI, installed EntityFramework.SqlServerCompact  installed to CodeCamper.Data and CodeCamper.Web  (NOTE: unsure if I need both)

enable-migrations -startupprojectname CodeCamper.Web -projectname CodeCamper.Data -enableautomaticmigrations

migrate(?) the sample data

I have no real idea what this migrations stuff is all about. It's one of the many topics which this code will encourage me to explore. I do know how to get the sample data to appear in the app

in CodeCamper.Data \ Migrations \ Configuration.cs

add

using CodeCamper.Data.SampleData;

change the Configuration class to it inherits from

CodeCamperDatabaseInitializer

remove the Configuration() parameterless constructor

CodeCamper.Data \ SampleData \ CodeCamperDataInitializer.cs

change the class so it inherits the commented out line

inherit from:

DbMigrationsConfiguration<CodeCamper.Data.CodeCamperDbContext>

and add: using System.Data.Entity.Migrations;

which is the class which Migrations\Configuration inherited from

CreateDatabaseIfNotExists<CodeCamperDbContext>      // when model is stable

???? why is migrations now disabled in the publish settings screen????

removed ctor from CodeCamperDbContext.cs

## Publish It

In solution explorer, right click "CodeCamper.web", click Publish... In VS2013, there is an option "Windows Azure Web Sites". Choose it, and log in to your Azure account

Create a "New..." website Add a unique site name, choose your locale, and create a new Database server, filling in name and credential fields

Go through each page of the wizard NOTE to self: "Execute code first migrations" is disabled. Because we haven't run it, the published app will have no data

Under the Settings Tab, you will see 2 entries for database. I have no idea why, but it caused me problems.

For the first, check "Use this connection string at runtime" AND "Execute Code First Migrations"

For the second one ("DefaultConnection"), uncheck "Use this connection string at runtime" WHen finished in the wizard, you'll be taken to a working web site