---
layout: help_doc
title: DEA .NET Release v1.x
tagline: Legacy Cloud Foundry \ DEA .NET (Droplet Execution Agent)
---

# DEA .NET Release v1.x

The DEA .NET has been released and is available. This has been released open source under the Apache 2.0 license. Here are the links to download and try it out:

[Download Installer x86](http://app.ironfoundry.me/download)

[Download Installer x64](http://app.ironfoundry.me/download)

[Grab the Code](https://github.com/IronFoundry/ironfoundry)

[View the Documentation](Legacy-Cloud-Foundry-DEA-NET-Documentation-v1.html)

Changes in version 1.6.0:

* Fixed memory leak caused by [Microsoft.Web.Administration.dll](https://connect.microsoft.com/VisualStudio/feedback/details/722272/microsoft-web-administration-servermanager-memory-leak)
* Fixed memory leak caused by timer event handler delegate not being unregistered.