---
layout: help_doc
title: Understanding the Cloud Foundry Command Line Interface
tagline: Iron Foundry V2 \ Getting Started
---

# Understanding the Cloud Foundry Command Line Interace (CLI)

At its most simple form, Cloud Foundry and Iron Foundry can be controlled from the command line using a [golang program](https://github.com/cloudfoundry/cli) called CF. This command line interface, or CLI, allows users to do almost everything necessary to deploy apps to Cloud Foundry, bind services to them, look at log files, and so on. And the things that you can't do through the CLI, the admin user can. That generally consists of user management, creating organizations and spaces, dealing with services and quotas, and advanced topics like that. 

This brief section will take you through the basics of finding, installing, and using CF to control your life throughout Iron Foundry. If you want the real, complete documentation for CF, you can find it on [Pivotal's](http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html) site.

### Installing the CLI
#### Finding CF
The newest versions of the CLI are always available through [github](https://github.com/cloudfolundry/cli). Once there, you can clone the CLI repo and build it for yourself, or you can install one of the [pre-built executables](https://github.com/cloudfoundry/cli#stable-release) on the page. I recommend the latter, because that prevents you from having to install Go, git, mecurial, and a lot of other packages.

#### Installing it
While the specifics different for each platform, the CLI should be available in some sort of [self-extracting bundle](https://github.com/cloudfoundry/cli#stable-release). Double click on it, or unzip it, or do whatever you do for your platform. The nice part about the CLI being written in Go is that all of its dependencies are statically linked into a single program - no shared libraries to download and  manage, no extra packages to install - it just works.

### CLI Concepts
The CF CLI is how most developers are going to interact with Iron Foundry nearly all of the time. The benefits of using the CLI over any sort of web interface are that it is very easy to use, it is conveniently available right from your keyboard, and it is scriptable. That last part could be the most important piece of this, as it allows you to create scripts to do all kinds of interesting and repetitive things. 

There is a basic lifecycle that developers will go through when interacting with Iron Foundry. It works like this.

* Point the CLI at the correct instance of Iron Foundry using `cf api` command
* Log into Iron Foundry using `cf login`
* Target the correct organization and space using `cf target`
* Push your application using `cf push`
* Bind one or more services to it using `cf bind-service`
* Check on the health of the app you pushed using `cf app`

And if you're ever lost or confused, there are a few different resources to help you find your way again.

* There is help inside the CLI using `cf help`, which prints out the list of commands and a quick summary of each. You can also get additional help for a particular command using `cf help <command>`
* Pivotal has [full documentation](http://docs.cloudfoundry.org/devguide/installcf) for the CF CLI on their site as well. 


