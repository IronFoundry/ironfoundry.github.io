---
layout: help_doc
title: Installation
tagline: Cloud Foundry V2 \ Ruby DEA
---

# Installation

Installation of the Ruby DEA is done via a downloadable archive and an installation script.

[Instructions are available here on GitHub](https://github.com/IronFoundry/dea_ng/blob/ironfoundry/WINDOWS.md)

Be sure to update your Cloud Controller's ```config/stacks.yml``` to recognize the ```mswin-clr``` stack:

```
vagrant@precise64:/vagrant$ cat cloud_controller_ng/config/stacks.yml
default: lucid64
stacks:
- name: lucid64
description: Ubuntu Lucid 64-bit
- name: mswin-clr
description: Microsoft .NET / Windows 64-bit
```