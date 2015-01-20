---
layout: post
title: Pairing on .NET Support for Diego in New York City
categories:
- Iron Foundry
- Cloud Foundry
- Diego
- .NET
tags: [tutorial]
status: publish
type: post
published: true
author: Chris Sterling
twitter: csterwa

---

This past week, [Brannon Jones](http://twitter.com/brannon) and [Chris Sterling](http://twitter.com/csterwa) from CenturyLink Cloud's PaaS team traveled to New York City. The goal of our visit was to pair with the Pivotal team adding .NET support to Diego and help define the implementation path going forward. Most of our time was spent with "The Four Daves" (David Varvel, David Morhovich, David Tengdin, and Dave Goddard) and [Mark Kropf](http://twitter.com/markkropf). It was fun getting embedded in the Pivotal culture and getting to know folks in the New York City office.

<img src="/img/blog/2015-01-12-pivotal-nyc-outside-front-door.jpeg"/>

The trip was definitely a success and as an outcome here are some high level decisions for the implementation of .NET support in Diego in the near term:

* The implementation will use Hostable Web Core (HWC) for launching pushed .NET applications in Diego. This is the
current implementation approach in [Iron Foundry](http://www.ironfoundry.org) and allows for more control of running jobs on Windows.
* Iron Foundry's implementation of [Container Host](https://github.com/IronFoundry/if_warden/tree/master/IronFoundry.Warden.ContainerHost) will be extracted as a NuGet package that can be used in both the current Iron Foundry working with existing releases of Cloud Foundry and also support Diego .NET.
* Brannon will pair with the Pivotal team adding .NET support in the future to integrate [Container Host](https://github.com/IronFoundry/if_warden/tree/master/IronFoundry.Warden.ContainerHost) into the open source repos for Diego .NET support.

Thank you to the Pivotal team for a great week and solid progress on our way towards .NET support in Diego. We're looking forward to future collaboration amongst our teams.

I took a bunch of great pictures while I was there but this picture of a throw pillow that I'll leave you with from the lobby at Pivotal in New York City was one of my favorites:

<img src="/img/blog/2015-01-12-unicorn-pillow.jpeg"/>
