---
layout: help_doc
title: Iron Foundry with Cloud Foundry Micro
tagline: Legacy Cloud Foundry \ Micro Cloud
---

# Iron Foundry with Cloud Foundry Micro

The micro instance enables you to do local development in .NET on the Micro Cloud Foundry instance. The Iron Foundry team has worked very hard to make this an easy transition without much hassle. You are four steps away from running your own cloud locally with .NET support:

**Step 1: Get all the bits needed to setup**

* Sign up on [Cloud Foundry](https://my.cloudfoundry.com/micro) for your micro cloud v1.1.0
* Download [Iron Foundry Micro Cloud](http://app.ironfoundry.me/download)

**Step 2: Get your Cloud Foundry Micro Cloud Working**

It is very easy to get your [Cloud Foundry Micro Cloud](https://my.cloudfoundry.com/micro) running. Here are the simple steps taken:

1. Unzip the virtual machine. Import it into VMWare Workstation, Player or Fusion.
1. Modify the VM settings and switch to "bridged" networking mode.
1. Start it up!
1. After it starts up select option 1 to configure.
	1. Set your password (*make sure to remember it!*)
	* Set DHCP or Static for network (we chose DHCP)
	* HTTP Proxy: (Choose none by hitting enter)
	* Enter in your configuration token (if you dont know it generate it [here](https://my.cloudfoundry.com/micro/dns))
	* After it is done updating your DNS it will Reinitialize the monit daemon and get everything installed. (can take up to 5 minutes)

![](/img/help/micro-cloud-iron-foundry-01.png)

Next thing to do is register a user within your Micro Cloud (Required).  Here is how to do this:
[http://start.cloudfoundry.com/infrastructure/micro/installing-mcf.html#registering-a-micro-cloud-foundry-user-with-vmc](http://start.cloudfoundry.com/infrastructure/micro/installing-mcf.html#registering-a-micro-cloud-foundry-user-with-vmc)

If you are still having trouble getting this part working please refer to the [Getting Started](http://support.cloudfoundry.com/entries/20316811-micro-cloud-foundry-getting-started-guide) guide from the Cloud Foundry team.

**Step 3: Get your Iron Foundry Micro Cloud Working**

Now that you have the Cloud Foundry Micro Cloud installed and up and running you can easily extend it to support .NET with the Iron Foundry Micro Cloud. The Iron Foundry Micro Cloud is a Windows Server 2008 R2 Standard Edition Server running in the Core role and has no software keys initialized which means you will need to provide your own license key to keep it running after the Windows trial period.

**Here are the steps to get started:**

1. Use 7-zip to unzip the Iron Foundry Micro Cloud VM and start it up in VMware Workstation, Player, or Fusion.
1. If VMWare asks if you have moved or copied the VM, choose “I copied it”.
1. It will show “Setup is starting services” as this is a Windows VM. After it goes through the inital setup it will continue and require your input
	* Set the timezone. Click Next
	* Accept the licensing terms. Click Next
	* It will now say that the users password must be changed before logging on the first time. Click OK and set the password (make sure to remember the password!)
1. After setting the password you will now be logged into the core terminal prompt. You can now enable Iron Foundry on your Cloud Foundry Micro Cloud. (Make sure your Cloud Foundry Micro Cloud is running at the same time)
	1. At the command prompt (C:\Users\Administrator) execute these commands:

		```
		C:\Users\Administrator>cd C:\IronFoundry\setup
		C:\IronFoundry\setup>RunSetup.cmd
		```

	1. Enter Micro CF Identity: This is your Cloud Foundry Micro Instance Url (example: jwray.cloudfoundry.me is the one we are using for this demo)
	1. Enter Micro CF Password: This is the password you entered when setting up your Micro Cloud in step 1.
	1. Once it is done installing press any key to exit

![](/img/help/micro-cloud-iron-foundry-02.png)

**Step 4: Push an Application and feel the love**

Now that you have been able to setup your Cloud Foundry instance running Iron Foundry you can now push and update your application by doing the following:

1. Download and install the VS 2010 extension from [here](http://app.ironfoundry.me/download).
1. Right click on your project and then go to “Push Cloud Foundry Application…
1. Choose “Manage Clouds...” to set up your new Micro Iron Foundry Cloud

	![](/img/help/micro-cloud-iron-foundry-03.png)

1. Choose “Manage Clouds...”

	![](/img/help/micro-cloud-iron-foundry-04.png)

1. Choose "Micro Cloud" from the dropdown at the bottom left. Be sure to replace "{username}" in the URL text box with the appropriate username entered in the Micro Cloud Foundry sign up. Enter your credentials and validate the connection

	![](/img/help/micro-cloud-iron-foundry-05.png)

1. When your account validates, close the “Add Cloud” and Explorer windows to return to the push dialog.
1. From the Push Cloud Foundry Application select the correct settings (you can see what we did below)
1. Cloud: Select the cloud you entered above.
1. Name: Enter in any name you want for the application.
1. URL: enter in the full url of the application. Here we will use [helloworld](http://helloworld23451.gofoundry.net/).jwray.cloudfoundry.me
1. Memory Limit: Select the amount of memory you want your application to use.
1. Instances: Select the number of instances you want your application running on.
1. Select the services you want to bind to your application such as a database.

	![](/img/help/micro-cloud-iron-foundry-06.png)

**Click the “Push” and it will package it up and push it live doing all the configuration of the services and application into Cloud Foundry with Iron Foundry.**