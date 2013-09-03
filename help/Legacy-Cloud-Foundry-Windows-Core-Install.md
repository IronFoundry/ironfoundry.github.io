---
layout: help_doc
title: Cloud Foundry with Iron Foundry (Windows Core) Install
tagline: Legacy Cloud Foundry \ Getting Started
---

# Cloud Foundry with Iron Foundry (Windows Core) Install

![](/img/help/cloud-foundry-windows-core-install-01.png)

Cloud Foundry has been taking the web by storm. PaaS is growing in popularity as more developers find the disruptively positive deployment scenarios that are possible over traditional environments. Cloud Foundry, primarily centered around Linux-based PaaS, now has a sibling called Iron Foundry.

Iron Foundry is an open source project available for the Windows Server Environments with the ability to run the full spectrum of .NET Web Applications, SQL Server, and more. IronFoundry places the Microsoft tool stack on an even footing with the Linux-based stacks.

![](/img/help/cloud-foundry-windows-core-install-02.png)

**Step 1:  Get IronFoundry Installed and Running by [Adron Hall](http://twitter.com/adron)**

The first thing you’ll need is to be sure to get a USB Thumb Drive or some mechanism to get the .NET 4.0 & IronFoundry Software onto the Windows Server 2008 Core Instance. If you’re using a full install of Windows Server 2008 then you can use the normal means to retrieve this software. The files you’ll want on the external storage include:

1. .NET 4.0 Framework for Server Core [dotNetFx40_Full_x86_x64_SC.exe](http://www.microsoft.com/download/en/details.aspx?id=22833)
2. IronFoundry DEA Service [IronFoundry.Dea.Service.x86.msi](http://www.ironfoundry.org/download) or [IronFoundry.Dea.Service.x64.msi](https://github.com/downloads/IronFoundry/ironfoundry/IronFoundry.Dea.Service.x64.msi)

Once you have the software downloaded to a medium to use, get a solid image of [Windows 2008 Server Core up and running](http://compositecode.com/2012/01/16/windows-server-2008-core-a-quick-run-down/). With the Windows 2008 Server Core command prompt get the following services installed and started with the following commands:

```
c:\Users\MyUserName\start /w ocsetup IIS-WebServerRole

c:\Users\MyUserName\start /w ocsetup WAS-NetFxEnvironment

c:\Users\MyUserName\start /w ocsetup IIS-ISAPIExtensions

c:\Users\MyUserName\start /w ocsetup IIS-ISAPIFilter

c:\Users\MyUserName\start /w ocsetup IIS-NetFxExtensibility

c:\Users\MyUserName\start /w ocsetup IIS-ASPNET

c:\Users\MyUserName\start /w ocsetup MicrosoftWindowsPowerShell

c:\Users\MyUserName\start /w ocsetup ServerCore-WOW64

c:\Users\MyUserName\start /w ocsetup NetFx2-ServerCore

c:\Users\MyUserName\start /w ocsetup NetFx2-ServerCore-WOW64
```

![](/img/help/cloud-foundry-windows-core-install-03.png)

After these services are started, copy the software off of the USB / Storage Device that has .NET 4.0 and the IronFoundry DEA. In the below copy command, “e:” is the storage device. 

```
e:\copy *.* c:\Users\MyUserName\
```

Now execute the .NET 4.0 Framework ([dotNetFx40_Full_x86_x64_SC.exe](http://www.microsoft.com/download/en/details.aspx?id=22833)) for Windows 2008 Server Core.

```
c:\Users\MyUserName\dotNetFx40_Full_x86_x64_SC.exe
```

From this point a standard Windows Wizard will display to step through the rest of the .NET 4.0 Server Core Installation. The next step is to enable IIS Remote Administration: 

```
c:\Users\MyUserName\reg add HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WebManagement\Server /v EnableRemoteManagement /t REG_DWORD /d 1
```

At this point it is actually a good idea to reboot the server to insure all the services start correctly and the registry setting takes effect. I’m sure that just simply restarting the services might work, but when playing with the registry I like to stay safe and insure everything is set and has taken effect.

After the reboot, start wmsvc.

```
c:\Users\MyUserName\net start wmsvc
```

Now kick off the [IronFoundry DEA Installation](https://github.com/downloads/IronFoundry/ironfoundry/IronFoundry.Dea.Service.x64.msi). When the wizard prompts for configuration information, enter the following:

1. NATS Host: 10.0.0.1
1. NATS Port: 4222
1. App Directory: C:\IronFoundry\apps
1. Droplet Directory: C:\IronFoundry\droplets
1. Install Directory: C:\Program Files\Iron Foundry\DEA

Once the wizard is complete, then go to c:\Program Files\Iron Foundry\DEA and run the DEA executable. This will start the IronFoundry DEA Service and insure it kicks off (self starting) anytime the server may be rebooted.

**Step 2:  Deploy an ASP.NET MVC Application by [Jared Wray](https://twitter.com/#!/jaredwray)**

Deploying an ASP.NET MVC application could not be easier when using Iron Foundry and the accompanying tools. There are three ways to deploy your application to Iron Foundry:

1. Visual Studio: The Iron Foundry plugin for Visual Studio allows you to push your application to any Cloud Foundry environment supporting .NET.
1. Cloud Foundry Explorer: The Cloud Foundry Explorer is a .NET Windows application that allows you to manage multiple cloud instances from a Windows desktop including all of the code and service deployment.
1. Command Line (VMC): This is the command line version with all of the features that you see from the plugin and explorer.

You can download these from Iron Foundry at: [http://www.ironfoundry.org/download](http://www.ironfoundry.org/download)

**Getting down to code a deployment...**

Lets first start out with downloading and installing the Visual Studio Plugin from Iron Foundry. Go to [http://www.ironfoundry.org/download](http://www.ironfoundry.org/download) and download the latest. After it is downloaded double click the file and do the install.  After the install is done open up Visual Studio and go to Tools > Extension Manager > From there you should see it installed:

![](/img/help/cloud-foundry-windows-core-install-03.png)

Lets go ahead and write a simple ASP.NET MVC (MVC 3 is being used in this and can be downloaded here: [http://www.asp.net/mvc](http://www.asp.net/mvc))) application by creating a simple “Hello World” application for testing. In Visual Studio do the following:

1. Go to File > New Project
1. Select the ASP.NET MVC 3 Web Application, set the name, location, and solution name and click “ok”
1. On the next screen you will be prompted with the “Project Template” and you can select “Empty” and your view engine as “Razor”.

Now we have setup the project we are going to write a simple page and publish it to an Iron Foundry instance.

1. From the Solution Explorer right click on the “Controllers” folder and go to Add > Controller.
1. The “Add Controller” dialogue window will come up and name it “HomeController” then click the “Add” button.
1. Next step is to add the Index View for the Home controller. You can do this by the following:
* Go to the “Views” folder > Create a folder called “Home” inside it
* Right click on the “Home” folder that was just created and Add > View. Name the View “Index.”

In the Views > Home > Index.cshtml file modify the code to be: 

![](/img/help/cloud-foundry-windows-core-install-04.png)

**(NOTE: Make sure you have compiled the site at least once before pushing it live for the first time.)**

With the [Visual Studio Plugin from Iron Foundry](http://www.ironfoundry.org/download) it is very easy to do a deployment/update from. All you will need to do is define your Cloud Foundry instance with Iron Foundry support and then “Push” your application.

Define your Cloud Foundry instance with Iron Foundry Support:

1. From Visual Studio Go to Tools > Cloud Foundry Explorer
1. From Cloud Foundry Explorer click the add new cloud button.
1. Enter in the following data:
* Server Name: The friendly name of the Cloud Foundry instance you plan to connect to. For this example we will use the

[Iron Foundry Trial](http://api.ironfoundry.me/signup) environment (api.gofoundry.net)

1. Runtime Environment:  Select the correct runtime environment (right now it should default to: Cloud Foundry Runtime v1.0).
1. Register/Logon Info: The Email, and Password are what you need to logon to your Cloud Foundry instance.
1. URL: To setup the url of your cloud foundry instance do the following:
1. Click on the “Manage Cloud...” button.
1. From the Manage Cloud Urls... window click “Add”
1. From the Add Cloud Url.. window type the Name and URL such as:
1. Name: Iron Foundry Trial
1. Url: [http://api.gofoundry.net](http://api.gofoundry.net/)
1. Click Ok.
1. From the Manage Cloud Urls... window verify that your URL has been added and click ok.

![](/img/help/cloud-foundry-windows-core-install-05.png)

5. Once you have entered the information correctly click to validate account and you will see an“Account Valid” message appear.
6. Close out the Cloud Foundry Explorer window as you are now ready to push your application!
7. Push your Application (The Cool Stuff!)

Now that you have been able to setup your Cloud Foundry instance running Iron Foundry you can now push and update your application by doing the following:

1. Right click on your project and then go to “Push Cloud Foundry Application...
2. ![](/img/help/cloud-foundry-windows-core-install-06.png)
3. From the Push Cloud Foundry Application select the correct settings:
4. Cloud: Select the cloud you entered above.
5. Name: Enter in any name you want for the application.
6. URL: enter in the full url of the application. Here we will use [helloworld23451.gofoundry.net](http://helloworld23451.gofoundry.net/).
7. Memory Limit: Select the amount of memory you want your application to use.
8. Instances: Select the number of instances you want your application running on.
9. Select the services you want to bind to your application such as a database.

![](/img/help/cloud-foundry-windows-core-install-07.png)

Click the “Push” and it will package it up and push it live doing all the configuration of the services and application into Cloud Foundry with Iron Foundry.