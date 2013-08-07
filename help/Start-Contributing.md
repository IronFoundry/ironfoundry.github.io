---
title: Start Contributing
---

# Start Contributing

It is always great to start contributing to an open source project. The Iron Foundry project is built upon the time, effort, and resources from developers and companies. 

## GIT Source Control
We use [Git](http://git-scm.com) and [GitHub](http://github.com/ironfoundry) to host the IronFoundry suite of projects. If you are new to Git, we recommend you give this [series of articles](http://www.lostechies.com/blogs/jason_meridth/archive/2009/06/01/git-for-windows-developers-git-series-part-1.aspx) a read.  Use [these instructions](http://help.github.com/win-set-up-git/) to set up Git on your Windows system.

## Getting the code
GitHub makes it very easy to fork projects so that you can make your own changes to a project and optionally get your changes incorporated back into the original project. If you want the source code so you can make changes to it, whether or not you are interested in contributing your changes back here, forking may be a good way to track what changes you make, and allow you convenient sharing of patches between the two projects.

First fork the project you're interested in on GitHub, then clone your forked repository to your your local machine.  After cloning an Iron Foundry repository, please ensure that core.autocrlf is set to true:

```
$ cd path/to/clone
$ git config core.autocrlf true
```

This will ensure that line endings remain correct on Windows systems.  Note that this setting for Iron Foundry is different than is typical for Windows-based GitHub projects.  We use this setting because of our close association with the [Cloud Foundry](https://github.com/CloudFoundry) project.

## Building the Iron Foundry solution
If you're interested in building the Iron Foundry project which contains the Cloud Foundry Explorer, the Visual Studio extension, and vcap extensions, you must first install these prerequisites:

* [WiX](http://wixtoolset.org/)
* [Visual Studio 2012 SDK (optional)](http://www.microsoft.com/en-us/download/details.aspx?id=30668)

You can then run **build.bat** in the root directory of the repository to build the code.  Dependencies will be resolved via NuGet.

## Contributor License Agreement
We welcome your contributions!

For significant contributions --  as with most open source projects -- we do require contributors to sign a Contributors License Agreement (CLA). The CLA is modeled after the Apache Foundation and Cloud Foundry CLAs, which have worked out well with both communities. 

Individual: [http://www.ironfoundry.org/cla-legal/ironfoundry-individual-contributors.pdf](http://www.ironfoundry.org/cla-legal/ironfoundry-individual-contributors.pdf)

Company: [http://www.ironfoundry.org/cla-legal/ironfoudry-company-contributors.pdf](http://www.ironfoundry.org/cla-legal/ironfoudry-company-contributors.pdf)
