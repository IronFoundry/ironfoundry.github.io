---
layout: post
title: Iron Foundry and Diego Collaboration
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
This past week, [Brannon Jones](https://twitter.com/brannon) traveled to San Francisco to pair with the [Cloud Foundry](http://cloudfoundry.org) team working on Diego. The main goal of the week was to help both teams ensure that the evolving architecture of Diego would support both Linux and Windows as OSs to which droplets could be deployed. Here is an excerpt from the vcap-dev status update by the Diego team from last week:

>Windows!: This past week we've been pairing with IronFoundry, starting
>on a Windows backend for Garden[2]. We had a prototype working in a
>couple days, leveraging the existing Warden.NET's container
>host[3]. We were then able to start the Executor on Windows, point it
>at our prototype, and spawn containers, run commands, and stream their
>output. This really demonstrates the flexibility we gain with Warden's
>(largely) platform-agnostic API and modular backend architecture.
>
>As part of this work we've split the Linux backend out into a separate
>repo[4], and Garden is now simply the library providing the server
>that the individual backends inject themselves into and
>start[5]. Extracting the Linux backend should make it clear to others
>how they can write their own.

and the [original post to vcap-dev](https://groups.google.com/a/cloudfoundry.org/forum/m/#!msg/vcap-dev/S6az7QPgriA/3fVUV6oCrzEJ), including URLs for the repos created.

Big thanks to everyone involved with this! Getting as far as they did in splitting out the Linux backend into a separate repo and making as much progress as was made on the Windows backend represents huge progress and validation for the architecture. Next up is replicating this collaboration on the remaining Windows pieces for Diego over the next couple of months.

