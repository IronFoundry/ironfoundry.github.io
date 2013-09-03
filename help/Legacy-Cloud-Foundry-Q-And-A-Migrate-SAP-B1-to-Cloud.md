---
layout: help_doc
title: Migrate SAP B1 instance &amp; .NET generated WSDL web service to the cloud?
tagline: Legacy Cloud Foundry \ Iron Foundry Q&amp;A
---

# Migrate SAP B1 instance &amp; .NET generated WSDL web service to the cloud?

## Question

via David Brown

Hello, we currently have our pre-production Grails app running on
cloudfoundry.

We also have a SAP Business One instance running in our datacenter.

We communicate with the SAP B1 instance via a web service provided by
the SAP B1 .net generated WSDL.

The WS client is running in our Grails app using the Grails Apache/CXF
plugin.

What are our chances of migrating the entire SAP B1 instance with the
.net generated WSDL to ironfoundry as a PaaS that is essentially in the
same cloud with our Grails app running on cloudfoundry?

## Answer

Your scenario could work using a private Iron Foundry installation.

The SAP B1 instance would have to run on a server that is accessible from your Grails application and .NET web service that you would push to your private cloud. For example if the SAP B1 server's IP address within the private cloud is 10.0.0.1 you would use this address to communicate with it - i.e. hard-code the address into the configuration of your .NET web service.

Then, the Grails application could communicate with the .NET web service via that service's public name within the cloud. If you push the .NET service to `sapnetservice.vcap.me` then the grails apps would use that name to communicate with the service, provided that the name resolves in DNS of course.