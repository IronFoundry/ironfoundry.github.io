---
layout: help_doc
title: Release Notes
tagline: Cloud Foundry V2 \ Ruby DEA
---

# Release Notes V1.0.0

This release of the Ruby DEA for windows is the initial release. It should be feature-compatible with the Ruby DEA running on Ubuntu.

Known issues:

File / directory services are not implemented yet. This requires some work to build and test the components written in Go

* Infrequent errors may happen in eventmachine (Errno::EBADF, Errno::ENOTSOCK). The team is investigating these errors and workarounds. Most of the time, a "cf stop" followed by a "cf start" will complete startup of your application. In some rare cases, the DEA service may require a restart.
* Please report any issues found as a support ticket on this site, or to GitHub issues here: [https://github.com/IronFoundry/dea_ng/issues](https://github.com/IronFoundry/dea_ng/issues)

Available for download from [http://www.ironfoundry.org/download](http://www.ironfoundry.org/download)

Source code is available on GitHub: [https://github.com/IronFoundry/dea_ng](https://github.com/IronFoundry/dea_ng)
