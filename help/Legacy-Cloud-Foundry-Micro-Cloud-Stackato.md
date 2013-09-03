---
layout: help_doc
title: Iron Foundry with Stackato from ActiveState
tagline: Legacy Cloud Foundry \ Micro Cloud
---

# Iron Foundry with Stackato from ActiveState

The micro instance enables you to do local development in .NET on the [Stackato Micro Cloud from ActiveState](http://www.activestate.com/stackato/download_vm) instance. The Iron Foundry team has worked very hard to make this an easy transition without much hassle. You are four steps away from running your own cloud locally with .NET support:

## Step 1: Get all the bits needed to setup

* Download [Stackato Micro Cloud from ActiveState](http://www.activestate.com/stackato/download_vm)
* Download [Iron Foundry Micro Cloud](http://app.ironfoundry.me/download)

## Step 2: First download and get the Stackato Micro Cloud Running.

It is very easy to get your [Stackato Micro Cloud](http://www.activestate.com/stackato/download_vm) running. Here are the simple steps taken:

1. Download the Stackato Micro Cloud here: [http://www.activestate.com/stackato/download_vm](http://www.activestate.com/stackato/download_vm)
1. Unzip the image to the location you want the image to execute from.
1. Set the network on the Stackato image to bridged.
1. Startup the Stackato Image.
1. When it boots up get the hostname and IP address and make a note of both values.
1. The hostname and IP address will need to be added to your hosts file, either ```/etc/hosts``` in OS-X or Linux and ```C:\Windows\System32\Drivers\hostsin``` Windows. Add the IP and host to the file with entries like these:
	```192.168.NNN.YYYY    stackato-XXXX.local api.stackato-xxxx.local testwebapp.stackato-xxxx.local```	
(add additional entries at the end for other web apps you intend to push)
1. Navigate to [http://stackato-XXXX.local](http://stackato-xxxx.local/) and it will redirect to the initial setup page where you enter an email address and password. These credentials are added to the Stackato Instance, so be sure to remember them.

## Step 3: Get your Iron Foundry Micro Cloud Working

Now that you have the Stackato Micro Cloud installed and up and running you can easily extend it to support .NET with the Iron Foundry Micro Cloud. The Iron Foundry Micro Cloud is a Windows Server 2008 R2 Standard Edition Server running in the Core role and has no software keys initialized which means you will need to provide your own license key to keep it running after the Windows trial period.

**Here are the steps to get started:**

1. Use 7-zip to unzip the Iron Foundry Micro Cloud VM and start it up in VMware Workstation, Player, or Fusion.
1. If VMWare asks if you have moved or copied the VM, choose “I copied it”.
1. It will show “Setup is starting services” as this is a Windows VM. After it goes through the inital setup it will continue and require your input
	1. Set the timezone. Click Next
	1. Accept the licensing terms. Click Next
	1. It will now say that the users password must be changed before logging on the first time. Click OK and set the password (make sure to remember the password!)
1. After setting the password you will now be logged into the core terminal prompt. You can now enable Iron Foundry on your Cloud Foundry Micro Cloud. (Make sure your Cloud Foundry Micro Cloud is running at the same time)
	1. Boot up the Micro Iron Foundry instance. It will prompt you for a password for the Administrator user.
	1. At the command prompt (C:\Users\Administrator) execute these commands:
	```
	C:\Users\Administrator>cd C:\IronFoundry\Setup
	C:\IronFoundry\Setup>RunSetup.cmd
	```
1. At the prompt enter your domain [stackato-XXXX.local](http://stackato-xxxx.local/), IP address and password.
1. It will then connect via ssh, patch the system, restart the cloud controller, and setup the local SQL provisioning services in the Iron Foundry VM.

![](/img/help/Iron-Foundry-with-Stackato-01.png)

Once the setup process is done you can use Cloud Foundry Explorer ([http://app.ironfoundry.me/download](http://app.ironfoundry.me/download)) to push an [ASP.NET](http://asp.net/) application. I’ve attached a sample [ASP.NET](http://asp.net/) application. Click the gear icon to add a cloud, click the green + button to add a New Server. Rename server to something and add an api url of [api.stackato-XXXX.local](http://api.stackato-xxxx.local/), email and password. Clicking ”Validate Account” should succeed. Once the cloud is added, you can use push and choose that cloud to publish to it. You should use “testwebapp” as the name since you added it to the hosts file above. Once pushed, you can visit [http://testwebapp.stackato-XXXX.local](http://testwebapp.stackato-xxxx.local/) to browse to your application, and [http://testwebapp.stackato-XXXX.local/env](http://testwebapp.stackato-xxxx.local/env) to see more detailed info.

## Step 4: Push an Application and feel the love

Now that you have been able to setup your Cloud Foundry instance running Iron Foundry you can now push and update your application by doing the following:

1. Download and install the VS 2010 extension from here.
1. Right click on your project and then go to “Push Cloud Foundry Application…
1. Choose “Manage Clouds...” to set up your new Micro Iron Foundry Cloud

	![](/img/help/Iron-Foundry-with-Stackato-02.png)


1. Choose “Manage Clouds...”

	![](/img/help/Iron-Foundry-with-Stackato-03.png)

1. Choose "Micro Cloud" from the dropdown at the bottom left. Be sure to replace "{username}" in the URL text box with the appropriate username entered in the Micro Cloud Foundry sign up. Enter your credentials and validate the connection

	![](/img/help/Iron-Foundry-with-Stackato-04.png)

1. When your account validates, close the “Add Cloud” and Explorer windows to return to the push dialog.
1. From the Push Cloud Foundry Application select the correct settings (you can see what we did below)
1. Cloud: Select the cloud you entered above.
1. Name: Enter in any name you want for the application.
1. URL: enter in the full url of the application. Here we will use [helloworld](http://helloworld23451.gofoundry.net/).stackato-XXXX.local
1. Memory Limit: Select the amount of memory you want your application to use.
1. Instances: Select the number of instances you want your application running on.
1. Select the services you want to bind to your application such as a database.

	![](/img/help/Iron-Foundry-with-Stackato-05.png)

**Click the “Push” and it will package it up and push it live doing all the configuration of the services and application into Cloud Foundry with Iron Foundry.**