---
layout: help_doc
title: Managing Applications From the Command Line
tagline: Legacy Cloud Foundry \ Getting Started
---

# Managing Applications From the Command Line

If you want to deploy and manage applications in Iron Foundry from the command line, you can use the VMC command-line tool which is offered as a Ruby gem.  You must install the [Iron Foundry version of this tool](http://rubygems.org/gems/vmc-IronFoundry) in order to take advantage of the additional runtimes, frameworks, and services offered by Iron Foundry.

**Prerequisites:**

* [Ruby 1.9.3](http://www.ruby-lang.org/en/downloads/) or greater
* [RubyGems](http://rubygems.org/) (usually pre-installed with Ruby)

**Installation:**

To install the Iron Foundry VMC gem on Windows first ensure that ruby.exe is in your PATH then run these commands:

	C:\>gem update --system
	C:\>gem install vmc-IronFoundry

**Use:**
For general documentation on how to use VMC, refer to the [Cloud Foundry VMC Quick Reference](http://docs.cloudfoundry.com/tools/vmc/vmc-quick-ref.html). 

**Caldecott**

If you wish to use the tunneling features of caldecott, you must install the [Ruby Dev Kit](http://rubyinstaller.org/add-ons/devkit/) as well. Install the Dev Kit to 'C:\RubyDevKit' after installing ruby to 'C:\Ruby193'.

	C:\Users\username>cd C:\RubyDevKit

	C:\RubyDevKit>set PATH=C:\Ruby193\bin;%PATH%

	C:\RubyDevKit>ruby dk.rb init
	[INFO] found RubyInstaller v1.9.3 at C:/Ruby193

	Initialization complete! Please review and modify the auto-generated
	'config.yml' file to ensure it contains the root directories to all
	of the installed Rubies you want enhanced by the DevKit.

	C:\RubyDevKit>ruby dk.rb review
	Based upon the settings in the 'config.yml' file generated
	from running 'ruby dk.rb init' and any of your customizations,
	DevKit functionality will be injected into the following Rubies
	when you run 'ruby dk.rb install'.

	C:/Ruby193

	C:\RubyDevKit>notepad config.yml

	C:\RubyDevKit>ruby dk.rb install
	[INFO] Updating convenience notice gem override for 'C:/Ruby193'
	[INFO] Installing 'C:/Ruby193/lib/ruby/site_ruby/devkit.rb'

	C:\RubyDevKit>

Now you will be able to install Caldecott:

	C:\>gem install caldecott
	Fetching: eventmachine-1.0.0-x86-mingw32.gem (100%)
	Fetching: addressable-2.2.8.gem (100%)
	Fetching: escape_utils-0.2.4.gem (100%)
	Temporarily enhancing PATH to include DevKit...
	Building native extensions.  This could take a while...
	Fetching: em-http-request-0.3.0.gem (100%)
	Building native extensions.  This could take a while...
	Fetching: em-websocket-0.3.8.gem (100%)
	Fetching: rack-1.4.1.gem (100%)
	Fetching: rack-protection-1.2.0.gem (100%)
	Fetching: tilt-1.3.3.gem (100%)
	Fetching: sinatra-1.3.3.gem (100%)
	Fetching: async_sinatra-0.5.0.gem (100%)
	Fetching: json-1.6.7.gem (100%)
	Building native extensions.  This could take a while...
	Fetching: uuidtools-2.1.3.gem (100%)
	Fetching: caldecott-0.0.5.gem (100%)
	Successfully installed eventmachine-1.0.0-x86-mingw32
	Successfully installed addressable-2.2.8
	Successfully installed escape_utils-0.2.4
	Successfully installed em-http-request-0.3.0
	Successfully installed em-websocket-0.3.8
	Successfully installed rack-1.4.1
	Successfully installed rack-protection-1.2.0
	Successfully installed tilt-1.3.3
	Successfully installed sinatra-1.3.3
	Successfully installed async_sinatra-0.5.0
	Successfully installed json-1.6.7
	Successfully installed uuidtools-2.1.3
	Successfully installed caldecott-0.0.5
	13 gems installed
