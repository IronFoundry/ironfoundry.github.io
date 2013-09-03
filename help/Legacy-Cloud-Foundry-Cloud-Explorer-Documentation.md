---
layout: help_doc
title: Cloud Foundry Explorer Documentation
tagline: Legacy Cloud Foundry \ Cloud Foundry Explorer
---

# Cloud Foundry Explorer Documentation

Installation
The following few steps illustrate the installation of the Cloud Foundry Explorer that works with both Cloud Foundry and Iron Foundry.

**Step 1: Find and download the MSI that is unique to your architecture**

[Iron Foundry Download Site](http://app.ironfoundry.me/download). Cloud Foundry Explorer is listed under "Developer Tools".

**Step 2: Launch the installer**

A. Installer

	![](/img/help/cloud-explorer-documentation-01.jpg)

B. Accept the license terms and start the install process

	![](/img/help/cloud-explorer-documentation-02.jpg)

	![](/img/help/cloud-explorer-documentation-03.jpg)

	![](/img/help/cloud-explorer-documentation-04.jpg)

C. Depending on your setup, you mind need to permit the install process to proceed.

	![](/img/help/cloud-explorer-documentation-05.jpg)

D. Continue during the rest of the install process..

	![](/img/help/cloud-explorer-documentation-06.jpg)
 
**Step 3: Verify the Install**
 
![](/img/help/cloud-explorer-documentation-07.jpg)

## Use

**Step 1: Launch Cloud Explorer**

![](/img/help/cloud-explorer-documentation-08.jpg)

**Step 2: Add a Cloud Connection**

Upon startup, use the gear icon to add a connection to `api.ironfoundry.me`:

![](/img/help/cloud-explorer-documentation-09.jpg)

You will be presented with the "Manage Clouds" screen (new in 1.6.0). To add a well-known cloud, use the dropdown at the bottom of the left side of the screen, with the cloud-plus icon. Select "Iron Foundry" to add a connection to this cloud. The url will be pre-filled to `http://api.ironfoundry.me`

Note: change the url to `http://api.ironfoundry.me`

A future update will change the default within Cloud Foundry Explorer

Enter the email address and password credentials that were mailed to you upon signup. Use the "Validate Account" button to double-check your entries.

![](/img/help/cloud-explorer-documentation-10.png)
 
When you choose "Ok", you will see this new cloud connection added to your explorer window.

![](/img/help/cloud-explorer-documentation-11.png)

Double-click the new connection to see an overview:

![](/img/help/cloud-explorer-documentation-12.png)

**Step 3: Push an application to Iron Foundry**

Use the "Push Application" button to push a new application to Iron Foundry:

![](/img/help/cloud-explorer-documentation-13.png)

In the dialog, choose the cloud to which to push. Then, choose an application name that does not contain spaces. The url to specify will be in the form `APPNAME.ironfoundry.me`, where `APPNAME` is the name you chose. Choose `Browse...` to pick the directory in which your built application resides. Note: this directory is the one in which a `Web.config` file and a `bin\` subdirectory exists.

Note: at this time you can only push ASP.NET applications using this tool. In addition, Iron Foundry only supports .NET applications at this point in time.

![](/img/help/cloud-explorer-documentation-14.png)

Once push completes, browse to `APPNAME.ironfoundry.me` to see your deployed application.