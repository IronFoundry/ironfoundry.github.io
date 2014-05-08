---
layout: help_doc
title: What is the CF command line to push a Windows app?
tagline: Iron Foundry V2 \ Additional Information
---

# What is the CF command line to push a Windows application?

Since Windows and .NET applications use a different stack than the standard Lucid64 stack employed by Linux applications, you need to explicitly name the stack to use when pushing a Windows or .NET application. The correct command line to use is `cf push <app> -s windows2012`.