---
layout: help_doc
title: Using the Visual Studio Extension
tagline: Legacy Cloud Foundry \ Getting Started
---

# Using the Visual Studio Extension

The solution build will create a ```CloudFoundry.Net.VsExtension.vsix``` file in the ```CloudFoundry.Net.VsExtension``` projects output directory.

Double-clicking this file will install the extension in Visual Studio.

To try out the extension, create a new ASP.NET MVC internet application in Visual Studio

![UI app](https://github.com/IronFoundry/ironfoundry/wiki/images/vs_app_new_project.png)

Note that you can access the "Cloud Foundry Explorer" application from the "Tools" menu:

![UI app](https://github.com/IronFoundry/ironfoundry/wiki/images/vs_app_tools_menu.png)

To push your application to Iron Foundry, right-click on the web application project and choose "Push Cloud Foundry Application":

![UI app](https://github.com/IronFoundry/ironfoundry/wiki/images/vs_app_tools_menu.png)

The "Push Cloud Foundry Application" dialog is the same as within the Explorer application.

![UI app](https://github.com/IronFoundry/ironfoundry/wiki/images/vs_app_push_dialog.png)