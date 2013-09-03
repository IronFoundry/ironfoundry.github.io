---
layout: help_doc
title: DEA Release v1.9
tagline: Legacy Cloud Foundry \ DEA .NET (Droplet Execution Agent)
---

# DEA Release v1.9

Updated recognized runtimes to include "clr40" and "clr20". The latest vcap-staging fork in the Iron Foundry code and api.ironfoundry.me adds these runtimes so you can select CLR 2 or 4 when pushing your application. For instance

	vmc push myaspnetapp --path C:\publish\myaspnetapp --runtime clr20

You can use the following command to set logging to debug while the .NET DEA is running as a Windows service:

	sc control ironfoundrydea 128

This command can retrieve statistics from running ASP.NET applications:

	vmc stats myaspnetapp