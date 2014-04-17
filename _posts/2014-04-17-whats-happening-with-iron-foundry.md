---
layout: post
title: What Is Happening with Iron Foundry
categories:
- .NET
- Iron Foundry
- Cloud Foundry
tags: []
status: publish
type: post
published: true
author: Brian Button
twitter: brianbuttonxp

---

It's an exciting and interesting time for the Iron Foundry project. This blog post will detail some of the ongoing activities in Iron Foundry, and talk a bit about the near term roadmap for the project.

## Cloud Foundry Incubation ##

Step one of the changes happened late in February, when IronFoundry V2 entered into the CloudFoundry Incubation Program. Jared posted about this [earlier](/2014/02/26/Iron-Foundry-Now-in-Cloud-Foundry-Incubation-Program/), and we're still working closely with the developers at CloudFoundry to make this a successful collaboration.

As part of that work, we had created branches off CloudFoundry v1.61 for our own version of the DEA, Warden, and Directory Server. We're maintaining this as our own fork, since that codeline in CF is going to be retired shortly. The Pivotal folks are making a pretty big architectural change to something called [Diego](https://docs.google.com/file/d/0BzowTjPNRrlzeHoyeTFoUWlla2M/edit), which is going to both rearchitect how staging and execution happen and replace a bunch of ruby code with golang.

Towards that end, one of the main collaborators on Iron Foundry traveled to San Francisco last week and paired with the Cloud Foundry developers to begin development of .NET extensions to Diego. Developers from the two projects are trying to work together closely to ensure that the extension points into the architecture that the CF devs built will work when implemented in a windows environment. The end goal of this is to allow Iron Foundry to be released as a full member of the Diego architecture at the same time, or closely thereafter, it is released by Cloud Foundry.

### Main Iron Foundry repositories ###

As a result of the ongoing work on Iron Foundry V2, we have created some new repositories and moved around some of the others. Here is a listing of the current repositories and what they're used for:

* [dea_ng](https://github.com/IronFoundry/dea_ng): This is our fork of the Cloud Foundry dea_ng repository. We branched off V1.61, so all of our code is based on that. This code will go away eventually, once our implementation of Diego is released and we're confident in it enough to retired this repository.
* [if_warden](https://github.com/cloudfoundry-incubator/if_warden): Our .NET implementation of a warden. It provides functionality similar to that of docker on linux.
* [cloudfoundry-buildpack-clr](https://github.com/cloudfoundry-incubator/cloudfoundry-buildpack-clr): The infrastructure used by Cloud Foundry to run .NET applications.

* [warden](https://github.com/ironfoundry/warden): This is our forked version of Cloud Foundry's warden repository. Will be retired with Diego.
* [eventmachine](https://github.com/IronFoundry/eventmachine): Our fork of the eventmachine repo, fixing some .NET-specific issues. Will also be retired with Diego.

* [if_release](https://github.com/IronFoundry/if_release): This single repository contains all other needed repositories as submodules. By cloning this and then running 'git submodule update --init', you can pull all of the Iron Foundry code out of github into a single source tree. The README.md for this repository also has the instructions describing how to install Iron Foundry onto a running windows VM.

* [if-service-broker](https://github.com/IronFoundry/if-service-broker): A .NET service broker to support provisioning SQL Server as a service for your application. The README.md file has the installation instructions for how to deploy this. Information about how to manage the service inside Cloud Foundry can be found in their [documentation](http://docs.cloudfoundry.org/services/managing-service-brokers.html).

We will be retiring all V1 Iron Foundry repos into our [attic](https://github.com/ironfoundry-attic) organization immediately to prevent confusion over what is current. They will still be available from there, but this will allow us to separate repositories with active development from those which are no longer in use.

## Updating IronFoundry.me ##

One of the next things we're going to work on is upgrading ironfoundry.me from Cloud Foundry V1 to a very recent version of Cloud Foundry V2. You'll see updates to the web site and a new instance of Cloud Foundry and Iron Foundry available at ironfoundry.me sometime soon. There are a number of steps that we're going to take to make this happen:

+ Update the ironfoundry.org web site to describe and link to the current implementation of Iron Foundry. We'll be updating links to github.com and source code to point to the correct repositories, updating the Sign Up process to create V2 accounts, and generally updating the appropriate sections of the content.
+ Retire the current ironfoundry.me instance. We will let everyone know of the cut-over date on which we'll turn off the existing ironfoundry.me and switch on the new version based on Cloud Foundry/Iron Foundry V2. User accounts will not be transferred to the new ironfoundry.me, so new accounts will be necessary. We're starting off fresh, so that we have a better handle on who the current users are, and what applications they have deployed.
+ Creating documentation about how to get started with ironfoundry.me, including where to find the right version of the golang-based CF client, and where to find lots of other good information on deploying to and running on ironfoundry.me.

## Supporting ironfoundry.me ##

As before, support will be offered through github issues in either the [if_release](https://github.com/ironfoundry/if_release) or [SQL Server broker](https://github.com/IronFoundry/if-service-broker) and through emails to the [ironfoundry google group](https://groups.google.com/forum/#!forum/ironfoundry). We intend to revive the original public trello board as a way to share what the Iron Foundry team is working on now and what is next on the road map. On that board, we welcome your input and your voting on future features.

We are very excited about a number of things revolving around the past, present, and future of Iron Foundry, including the progress we've made on Iron Foundry over the past couple of months, the collaboration we've started with Pivotal on the DEA and warden pieces we've been working on in the new Diego architecture and other projects moving forward, and the future of Iron Foundry and ironfoundry.me down the road.

But even with all those things going on, we still need the help of the Iron Foundry community. In fact, _especially_ with all these things going on, we need the community's help. Download Iron Foundry, use it, tell us what you think, add some new feature to it and send us a pull request, and maybe even tell your friends about it. It's going to take our entire community to make this project successful, so please join in!
