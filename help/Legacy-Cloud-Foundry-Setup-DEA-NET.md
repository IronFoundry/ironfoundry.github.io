---
layout: help_doc
title: Setting up and running the .NET DEA
tagline: Legacy Cloud Foundry \ DEA .NET (Droplet Execution Agent)
---

# Setting up and running the .NET DEA

Windows pre-requisites. You can use the [Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx) to set up IIS, .NET 4 and ASP.NET MVC.

* Server 2008 or 2008 R2
* IIS role installed
* .NET 4.0
* (suggested) ASP.NET MVC

Download the MSI installer from [http://app.ironfoundry.me/download](http://app.ironfoundry.me/download)

You'll need to know the following information prior to installation:

* IP address of your Cloud Controller
* Port that NATS is running on (most likely 4222)
* NATS user and password. They will be found in the `nats_server.yml` or the `cloud_controller.yml` file, in the `mbus:` setting. If you have built your Cloud Foundry environment from `vcap_dev_setup`, the credentials will be `nats/nats`.
Enter these values in the installation UI. The service will be installed and set to automatically start. You should be able to confirm successful start by looking in the log files here:

	C:\Program Files\Iron Foundry\DEA\logs

You can also install the MSI from the command line using properties:

	C:\>start /wait msiexec /i IronFoundry.DEA.Service.x64.msi NATSHOST=10.0.0.1 NATSUSER=nats NATSPASSWORD=nats /l*v install.log