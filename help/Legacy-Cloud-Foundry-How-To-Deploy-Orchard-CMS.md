---
layout: help_doc
title: Deploy Orchard CMS on Iron Foundry
tagline: Legacy Cloud Foundry \ How To
---

# Deploy Orchard CMS on Iron Foundry

[Orchard](http://orchardproject.net/) is a free, open source, community-focused project aimed at delivering applications and reusable components on the ASP.NET platform. The Orchard project as a very active and vibrant community that is actively developing and also using it for personal and commercial offerings.

[Iron Foundry](http://www.ironfoundry.org/) is an open source project  that extends .NET to [Cloud Foundry](http://www.cloudfoundry.org/) (The Open Platform as a Service). available for the Windows Server Environments with the ability to run the full spectrum of .NET Web Applications, SQL Server, and more. Iron Foundry places the Microsoft tool stack on an even footing with the Linux-based stacks. This platform is all open source and can be deployed anywhere. Today we are going to use the free trial environment provided by the Iron Foundry project.

With Iron Foundry and Cloud Foundry Orchard can scale within minutes to handle load on the system. This also gives an environment for rapid testing and staging of your application.

In four easy steps you can deploy and start configuring your Orchard CMS instance on Iron Foundry:

**Step 1:  Download Orchard CMS**

To download Orchard just go to the [Download Page](http://orchardproject.net/download) and then select the “Download as a zip” it is about 8MB in size. It will then ask you to agree to the terms.

**Step 2:  Make changes to be supported on Iron Foundry**

Go ahead and unzip it to your temporary directory.
You can read more about the manual install here: [http://docs.orchardproject.net/Documentation/Manually-installing-Orchard-zip-file](http://docs.orchardproject.net/Documentation/Manually-installing-Orchard-zip-file)

**Step 3:  Sign up and Deploy to Iron Foundry**

1. Sign up for your free account on [Iron Foundry](http://app.ironfoundry.me/signup) so you can test your deployment. (Note: this can take up to 24 hours to get your account activated.)
1. Once your account is activated you can also download the [Cloud Foundry Explorer](http://app.ironfoundry.me/download) from Iron Foundry.
1. After installing the Cloud Foundry explorer you will need to run the application.
1. Upon startup, use the gear icon to add a connection to api.gofoundry.net:
	![](/img/help/deploy-orchard-cms-01.png)

1. You will be presented with the "Manage Clouds" screen (new in 1.6.0). To add a well-known cloud, use the dropdown at the bottom of the left side of the screen, with the cloud-plus icon. Select "Iron Foundry" to add a connection to this cloud. The url will be pre-filled to [http://api.gofoundry.net](http://api.gofoundry.net/)
1. Enter the email address and password credentials that were mailed to you upon signup. Use the "Validate Account" button to double-check your entries
	![](/img/help/deploy-orchard-cms-02.png)

1. When you choose "Ok", you will see this new cloud connection added to your explorer window.
	![](/img/help/deploy-orchard-cms-03.png)
1. Double-click the new connection to see an overview that will be displayed on the right.
	![](/img/help/deploy-orchard-cms-04.png)
1. Next you will want to create an SQL instance to use. Main Iron Foundry Production tab at the bottom switch to “Applications” view.
1. On the services click the button to create a new service. Create a name for it and then from the drop down select MS SQL.
	![](/img/help/deploy-orchard-cms-05.png)
1. Use the "Push Application" button to push a new application to Iron Foundry:
	![](/img/help/deploy-orchard-cms-06.png)
1. In the dialog, choose the cloud to which to push. Then, choose an application name that does not contain spaces. The url to specify will be in the form APPNAME.gofoundry.net, where APPNAME is the name you chose. Choose Browse... to pick the directory in which you unziped your orchard application. Note: this directory is the one in which a Web.config file and a bin\ subdirectory exists.
	![](/img/help/deploy-orchard-cms-07.png)
1. Once push completes, browse to APPNAME.gofoundry.net to see your deployed application.
 
**Step 4: Setup your new Orchard Instance**

You should be able to browse to your new orchard install at your application url ([http://APPNAME.gofoundry.net](http://appname.gofoundry.net/)) where you will see a getting started page:

![](/img/help/deploy-orchard-cms-08.png)

When you get to the screen below you are going to want to select to deploy SQL server and put in the connection string. To get the connection string you need to do the following:

1. Go back to the Cloud Foundry Explorer
1. Once there browse to your cloud and then browse to your application
1. Once you have expanded to see the files double click on the web.config file which will open for you. In there you will see more entries added. All you need to do is copy the SQL server configuration settings and then put it into the orchard setup screen.

![](/img/help/deploy-orchard-cms-09.png)