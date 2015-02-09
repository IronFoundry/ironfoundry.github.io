---
layout: post
title: Diego Windows Update
categories:
- Iron Foundry
- Cloud Foundry
- Diego
- .NET
tags: []
status: publish
type: post
published: true
author: Chris Sterling
twitter: csterwa

---

On Wednesday, February 4th, 2015, the Cloud Foundry Foundation held the Community Advisory Board (CAB) meeting.
There is a great review of the entire Cloud Foundry CAB meeting [here](http://www.activestate.com/blog/2015/02/cloud-foundry-advisory-board-meeting-2015-february).

On the Windows Diego front, [Brannon Jones](http://twitter.com/brannon) and [Marcel Ortiz](https://github.com/mosoto),
both team members at CenturyLink Cloud, refactored the Iron Foundry
[Container Host](https://github.com/IronFoundry/if_warden/tree/master/IronFoundry.Container.Host)
and extended aspects of Iron Foundry's [Warden](https://github.com/IronFoundry/if_warden) into a single
library that can be refitted back into Iron Foundry and also be used by Diego Windows. This work along with
the great collaboration with the Diego Windows team in New York City offices of Pivotal has lead to significant
progress in the delivery of Diego Windows.

As a result of the work between the teams at [CenturyLink Cloud](http://www.centurylinkcloud.com/) and
[Pivotal](http://www.pivotal.io/), there are now 3 new additions to the Cloud Foundry Incubator by
unanimous vote at the CAB meeting:

* "Containerizer": A [Garden](https://github.com/cloudfoundry-incubator/garden) backend to support Windows container isolation.
* Garden Windows: Windows specific implementation of [Garden](https://github.com/cloudfoundry-incubator/garden) API
* Windows App Lifecycle: The Windows specific implementation of Diego [App Lifecycles](https://github.com/cloudfoundry-incubator/diego-design-notes#app-lifecycles)

The cross-collaboration between our teams at CenturyLink Cloud and Pivotal has generated valuable
output within only a few weeks. We're having fun working with the Cloud Foundry Foundation on
a power open source platform that is now well under way towards native Windows application support.
