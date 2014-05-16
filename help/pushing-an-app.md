---
layout: help_doc
title: Pushing an app
tagline: Iron Foundry V2 \ Advanced Topics
---
# Pushing an App into Cloud Foundry
The most basic thing a developer can do is to push an application into Cloud Foundry to deploy it to the internet at large. This simple action starts a chain of events that culminates with an application being available to people through their web browser. The rest of this article will describe how to push an application, and detail the options available when you do push  your application. We'll also talk a little bit about an application manifest, which allows you to specify options one time, in the manifest file, so that you don't have to repeat them each time you push your application.

### Pushing an application
The `cf push` command is used to push an application in Cloud Foundry. It has a lot of options to it, all of which are used to control details about the application being pushed.

	NAME:
	   push - Push a new app or sync changes to an existing app
	
	ALIAS:
	   p
	
	USAGE:
	   Push a single app (with or without a manifest):
	   cf.exe push APP [-b BUILDPACK_NAME] [-c COMMAND] [-d DOMAIN] [-f MANIFEST_PATH]
	   [-i NUM_INSTANCES] [-k DISK] [-m MEMORY] [-n HOST] [-p PATH] [-s STACK] [-t TIMEOUT]
	   [--no-hostname] [--no-manifest] [--no-route] [--no-start]
	
	   Push multiple apps with a manifest:
	   cf.exe push [-f MANIFEST_PATH]
	
	
	OPTIONS:
	   -b                   Custom buildpack by name (e.g. my-buildpack) or GIT URL (e.g. https://github.com/heroku/heroku-buildpack-play.git)
	   -c                   Startup command, set to null to reset to default start command
	   -d                   Domain (e.g. example.com)
	   -f                   Path to manifest
	   -i                   Number of instances
	   -k                   Disk limit (e.g. 256M, 1024M, 1G)
	   -m                   Memory limit (e.g. 256M, 1024M, 1G)
	   -n                   Hostname (e.g. my-subdomain)
	   -p                   Path of app directory or zip file
	   -s                   Stack to use (a stack is a pre-built file system, including an operating system, that can run apps)
	   -t                   Start timeout in seconds
	   --no-hostname        Map the root domain to this app
	   --no-manifest        Ignore manifest file
	   --no-route           Do not map a route to this app
	   --no-start           Do not start an app after pushing
	   --random-route       Create a random route for this app
	 
In its most basic form, `cf push app_name`, will start the deployment process for an application, giving it the name provided by the command. The CLI pushes the content of the current directory into Cloud Foundry, which then follows its launching process to start your application. The default values for memory size, disk and CPU limits, and so on, are set as part of your organization's quota or through bosh when the system is deployed.

Many of these settings can be changed, either through the command line as shown above, or by setting them in an application manifest file, which contains these same settings in a more persistent format.

#### Pushing a Simple .NET Application
Starting with a trivial example of an ASP.Net MVC application, let's push that to ironfoundry.me. 

___Step 1___
Build your application as normal. Nothing changes here for a simple, self-contained web site. Just build it.

___Step 2___
Publish it so that it can be pushed into Cloud Foundry. You can do this through through the Build menu, choosing Publish from there. When you select that, a dialog box will pop up that takes you through a short wizard. You'll want to:

1. Create a new profile
2. Choose File System as your target and a file location as the destination
3. Select the build type to publish (Debug/Release/etc)
4. Select Publish to publish to the selected file system location.

___Step 3___
The final step is to push the application to ironfoundry.me. This uses the CF command line tool, so you'll need that [installed](/help/understanding-cli.html), and you'll need a comand window like powershell. Open that command window and go to the file system directory you chose in the last step.

Log into your ironfoundry.me account, target your organization and space, as described [here](/help/logging-in.html), and you should be ready to push your application.

Once logged in, enter the following command: `cf push <app_name> -s windows2012`, where app_name is some descriptive name you've given to your application, and `-s windows2012` tells Cloud Foundry to use the Iron Foundry stack to deploy your code. The app name you choose does not have to be the name you chose in Visual Studio.NET - it can be any name. This name becomes part of the URL you'll use to access your application once pushed, as in MyApp.ironfoundry.me.

What you'll see next is Cloud Foundry reporting the successes of the subsequent steps that are part of staging and starting an application.

	PS C:\deploy\SimpleWebSite> cf push SimpleWebSite -s windows2012
	Using stack windows2012...
	OK

The application is being pushed with the Iron Foundry deployment instructions

	Creating app SimpleWebSite in org bbutton / space development as bbutton@agilestl.com...
	OK
	
	Creating route simplewebsite.beta.ironfoundry.me...
	OK
	
	Binding simplewebsite.beta.ironfoundry.me to SimpleWebSite...
	OK
	
Cloud Foundry successfully created its internal structures to represent the application.
	
	Uploading SimpleWebSite...
	Uploading app files from: C:\deploy\SimpleWebSite
	Uploading 6.6M, 52 files
	OK
	
The code was successfully uploaded to ironfoundry.me.
	
	Starting app SimpleWebSite in org bbutton / space development as bbutton@agilestl.com...
	OK
	
	1 of 1 instances running
	
	App started
	
The application was successfully started.
	
	Showing health and status for app SimpleWebSite in org bbutton / space development as bbutton@agilestl.com...
	OK
	
	requested state: started
	instances: 1/1
	usage: 512M x 1 instances
	urls: simplewebsite.beta.ironfoundry.me
	
	     state     since                    cpu    memory           disk
	#0   running   2014-05-16 05:29:00 PM   0.0%   205.6M of 512M   0 of 1G
	
And finally, we see a summary of the application as it is running. This represents a successful deployment of an application.

___Step 4___ And for proof, here is the running application:

<img src="/img/help/PublishedApp.png"/>

####Using Options to Alter Deployment
Now that the app is successfully deployed, we can look at how we can use the options shown above to change aspects of its deployment. There are a lot of options, all of them useful for different scenarios, but there are only a few that are useful for this basic scenario.

___Changing the Memory Limit___ Every application that is launched counts against the memory limit for an organization. You can limit the amount of memory that an application is allowed to use, however, through the `-m` option, which specified the maximum memory limit for that app. This value can be specified as any value, suffixed with either M or G (megabyte or gigabyte).

___Specifying a Different Hostname___ By default, the URL created by pushing an app into Cloud Foundry looks like app_name.ironfoundry.me. This can be changed, however, using the `-n hostname` option, which allows you to specify a different hostname for your application. This is useful the application name is too long or too hard to remember for a URL, and you want something shorter.

___Specifying the Number of Instances___ Unless told differently, Cloud Foundry starts a single instance of your application. This can be changed with the `-i instance_count` option, which allows multiple instances to be started at once. This is useful for enhancing the availability of your application by having multiple web servers handling requests to the same URL. The Router component of Cloud Foundry will automatically route users to any one of the servers handling requests for that URL.

___Choosing the Stack___ As seen in the example above, the `-s stack-name` option allows you to give a hint to Cloud Foundry about what it takes to deploy an application. If you do not provide this option the lucid64 stack is used by default, which provides instructions for how to deploy several kinds of applications onto Linux. In order to deploy to windows, you _must_ use `-s windows2012`.

Here is an example of using all of those options as once to relaunch our app:

	PS C:\deploy\SimpleWebSite> cf push SimpleWebSite -i 5 -m 256M -n simple -s windows2012
	
and just those pieces of the deployment process that show their effects:

	Using stack windows2012...
	OK
	
	Creating route simple.beta.ironfoundry.me...
	OK
	
	Binding simple.beta.ironfoundry.me to SimpleWebSite...
	OK

	5 of 5 instances running
	
And the final result of our `cf push`:
	
	App started
	
	Showing health and status for app SimpleWebSite in org bbutton / space development as bbutton@agilestl.com...
	OK
	
	requested state: started
	instances: 5/5
	usage: 256M x 5 instances
	urls: simplewebsite.beta.ironfoundry.me, simple.beta.ironfoundry.me
	
	     state     since                    cpu    memory           disk
	#0   running   2014-05-16 06:19:53 PM   0.0%   203.9M of 256M   0 of 1G
	#1   running   2014-05-16 06:19:58 PM   0.0%   203.8M of 256M   0 of 1G
	#2   running   2014-05-16 06:19:58 PM   0.0%   203.7M of 256M   0 of 1G
	#3   running   2014-05-16 06:19:53 PM   0.0%   204.3M of 256M   0 of 1G
	#4   running   2014-05-16 06:19:58 PM   0.0%   203.9M of 256M   0 of 1G
	
#### Using a Manifest to Simplify Deployment

While having all of those options available is powerful, it can be burdensome to type them in every time you want to push your app. To make this easier, you can define a manifest file that contains all of your options, and Cloud Foundry will read them from there. Here is a manifest file that does the same thing as our command line:

	---
	applications:
	- name: SimpleWebSite
	  instances: 5
	  memory: 256M
	  host: simple
	  stack: windows2012
	  
Once the manifest file is created and saved as manifest.yml, the app can then be pushed by simply entering `cf push`.
