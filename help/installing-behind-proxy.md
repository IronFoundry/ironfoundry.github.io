---
layout: help_doc
title: How Do I Install Iron Foundry Behind a Proxy?
tagline: Iron Foundry V2 \ Additional Information
---

# How do I install Iron Foundry behind a proxy?

Installing Iron Foundry behind a proxy server requires a few minor changes in the installation steps, mostly due to the use of Linux-based tools like git and ruby. Normally, windows-based programs would pick up the proxy server credentials and address from Internet Options, and things would just work. Since we have the extra tools, we have to specify our proxy credentials and address a few different ways. Fortunately this is easy to do, and once you do it the installation should just work again.

## Changes for installing behind a proxy
Three discrete changes are all that is necessary to deploy behind a firewall:

1. Open Internet Explorer, Internet Options, go into the Connections tab, and configure your proxy server in the appropriate way. That might be by allowing for autodiscovery, you may have a configuration script, or may have to set it up manually. Save that change and exit.
2. Open a powershell window and enter `$env:HTTP_PROXY = "proxy information"`, where the double quotes are important, since this is a string.
3. Create a file in the logged in user's home directory called .gitconfig. In that file, put this content, replacing 127.0.0.1.8118 with the credentials and address of your proxy server.

```
[http]  
	proxy = http://127.0.0.1:8118    
[https]  
	proxy = http://127.0.0.1:8118  
```

Once those three steps are completed, you can run through the installation steps as written in the [README](https://github.com/ironfoundry/if_release/#ironfoundry-release) file.
