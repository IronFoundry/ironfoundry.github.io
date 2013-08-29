---
layout: help_doc
title: cf Command Example
tagline: Cloud Foundry V2 \ Cloud Foundry V2 Local Dev
---

# cf Command Example

Instructions for using the cf command line application on Windows:

* Download a Ruby 193 x86 build from [http://rubyinstaller.org/downloads](http://rubyinstaller.org/downloads)
* Extract to ```C:\Ruby193``` and add ```C:\Ruby193\bin``` to your system PATH
* (Optional) do some updates and install bundler with these commands:

```
gem update --system
gem install bundler
```

* Install the cf client:

```
gem install cf
```

* Target your installation and push an ASP.NET application:

```
cf target api2.vcap.me
cf login
cf push testaspnet --path C:\projects\published\TestApp --stack mswin-clr
```

* At this point your application will stage and be deployed. Since the file and directory services are works-in-progress, your client may not receive notification that deployment is complete. Cancel with CTRL-C and check the status of your app:

```
cf apps
```

If you continue to have issues deploying your application, a cf stop followed by a cf start can resolve it. Please report these and other issues using the support system on this site.