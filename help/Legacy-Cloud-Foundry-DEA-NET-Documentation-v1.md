---
layout: help_doc
title: DEA .NET Documentation v1.0
tagline: Legacy Cloud Foundry \ DEA .NET (Droplet Execution Agent)
---

# DEA .NET Documentation v1.0

This is the first release for the DEA built using .NET. It is fully compatible with the Ruby DEA. We will be adding more documentation shortly.

Example command lines:

	C:\>start /wait msiexec /q /i IronFoundry.Dea.Service.x64.msi /l*v install.log NATSHOST=10.0.0.1 NATSPORT=4222 LOCALROUTE=10.0.0.2 APPDIR=C:\IronFoundry\apps DROPLETDIR=C:\IronFoundry\droplets INSTALLDIR="C:\Program Files\Iron Foundry\DEA"

The above command line will install the DEA and wait for completion. Verbose logging will be in install.log

Properties you can pass: 

NATSHOST - the IP address of your cloud controller.

NATSPORT - the port on which the CC is listening. Default is 4222.

LOCALROUTE - one of your local machine's IP addresses.

APPDIR - full path to where the apps will be deployed and IIS websites directed to. Default is C:\IronFoundry\apps

DROPLETDIR - full path to where droplet packages will be unzipped before copying to APPDIR. Default is C:\IronFoundry\droplets.

INSTALLDIR - full path to the installation directory for the DEA. Default value is shown above for x64.