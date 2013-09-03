---
layout: help_doc
title: Using Caldecott with MS SQL Server
tagline: Legacy Cloud Foundry \ How To
---

# Using Caldecott with MS SQL Server

Recently Caldecott support was added to the vmc repository within Iron Foundry. If you're not familiar with what Caldecott provides, a good overview is available on the [Cloud Foundry blog](http://blog.cloudfoundry.com/post/12928974099/now-you-can-tunnel-into-any-cloud-foundry-data-service).

To use Caldecott on Iron Foundry from a Windows machine to connect to a provisioned MS SQL database, follow these steps.

Install Ruby for Windows from [Ruby Installer](http://rubyinstaller.org/downloads). This is tested using version 1.9.3. During installation you can either add ruby to your PATH or add it manually later.

Run the following commands from a command prompt. You should ensure that ruby and sqlcmd are in your PATH as well.

Checking ruby version:

	C:\>ruby --version
	ruby 1.9.3p125 (2012-02-16) [i386-mingw32]

Ensuring that sqlcmd.exe is in your PATH. If not, it is located by default at

C:\Program Files\Microsoft SQL Server\100\Tools\Binn\sqlcmd.exe

	C:\>sqlcmd /?
	Microsoft (R) SQL Server Command Line Tool
	Version 10.50.2500.0 NT x64
	Copyright (c) Microsoft Corporation. All rights reserved.

Install the vmc-IronFoundry gem

	C:\>gem install vmc-IronFoundry --pre
	Fetching: vmc-IronFoundry-0.3.16.IF.1.gem (100%)
	Successfully installed vmc-IronFoundry-0.3.16.IF.1
	1 gem installed
	Installing ri documentation for vmc-IronFoundry-0.3.16.IF.1...
	Installing RDoc documentation for vmc-IronFoundry-0.3.16.IF.1...

You also need to install the Caldecott gem. Currently one of its dependencies has to be explicitly installed first:

	C:\>gem install eventmachine --pre
	Fetching: eventmachine-1.0.0.beta.4.1-x86-mingw32.gem (100%)
	Successfully installed eventmachine-1.0.0.beta.4.1-x86-mingw32
	1 gem installed
	Installing ri documentation for eventmachine-1.0.0.beta.4.1-x86-mingw32...
	Installing RDoc documentation for eventmachine-1.0.0.beta.4.1-x86-mingw32... 

Then you can install Caldecott:

	C:\>gem install caldecott
	Fetching: caldecott-0.0.5.gem (100%)
	Successfully installed caldecott-0.0.5
	1 gem installed
	Installing ri documentation for caldecott-0.0.5...
	Installing RDoc documentation for caldecott-0.0.5...

Target api.ironfoundry.me and log in to your account

	C:\>vmc target api.ironfoundry.me
	Successfully targeted to [http://api.ironfoundry.me]
	C:\>vmc login --email foo@bar.com --passwd XXXYYYZZZ
	Attempting login to [http://api.ironfoundry.me]
	Successfully logged into [http://api.ironfoundry.me]

Provision an MS SQL database

	C:\>vmc create-service mssql
	Creating Service [mssql-c902d]: OK

Tunnel to your database

	C:\>vmc tunnel mssql-c902d sqlcmd
	Deploying tunnel application 'caldecott'.
	Uploading Application:
	 Checking for available resources: OK
	 Packing application: OK
	 Uploading (1K): OK
	Push Status: OK
	Binding Service [mssql-c902d]: OK
	Staging Application 'caldecott': OK
	Starting Application 'caldecott': OK
	Getting tunnel connection info: OK
	Service connection info:
	 username : uxeBbNM0jYAFS
	 password : psOmxGWibimeX
	 name : d7dedaf7e01ae42568c07c44ec30bff99
	Starting tunnel to mssql-c902d on port 10000.
	Launching 'sqlcmd -S localhost,10000 -U uxeBbNM0jYAFS -P psOmxGWibimeX -d d7dedaf7e01ae42568c07c44ec30bff99'
	1>

You can now run commands from within sqlcmd against your database!

	1> select @@VERSION
	2> GO
	Microsoft SQL Server 2008 R2 (SP1) - 10.50.2500.0 (X64)
	 Jun 17 2011 00:54:03
	 Copyright (c) Microsoft Corporation
	 Enterprise Edition (64-bit) on Windows NT 6.1 <X64> (Build 7601: Service Pack 1) (Hypervisor)
	In addition, you can use the displayed connection information to connect via SQL Management Studio. Just use localhost,10000 as the "Server name". Be sure to start the tunnel first and keep it open during the time you're using

Management Studio. Quitting sqlcmd will close the tunnel.

![](/img/help/using-caldecott-mssql-server.png)