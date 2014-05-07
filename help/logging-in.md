---
layout: help_doc
title: How to Log Into Iron Foundry
tagline: Iron Foundry V2 \ Getting Started
---
# The Mechanics of Logging Into Iron Foundry
There are two separate, but equally important, steps to logging into any Cloud Foundry or Iron Foundry instance. The first involves pointing CF to the correct instance, and the second allows the user to provide their credentials to the system. Both of these are required before someone can successfully access the system.

### Pointing to the Correct Instance
CF can control as many different Iron Foundry instances as desired, but it can only be authenticated against one of them at a time. CF stores a single set of login credentials in $HOME/.cf, or the equivalent on Windows, %USERPROFILE%\\.cf, which prevents you from being logged into multiple instances at the same time.

You can change the Iron Foundry API endpoint to which  you are pointing using `cf api`.

	PS C:\Users\bbutton> cf help api
	NAME:
	   api - Set or view target api url
	
	USAGE:
	   cf.exe api [URL]
	   
Using this, I can point CF to the API endpoint for ironfoundry.me -

	PS C:\Users\bbutton> cf api api.beta.ironfoundry.me
	Setting api endpoint to api.beta.ironfoundry.me...
	OK
	
	API endpoint: https://api.beta.ironfoundry.me (API version: 2.2.0)
	Not logged in. Use 'cf.exe login' to log in.
	
This command targeted me at the current installation of Iron Foundry, beta.ironfoundry.me. From this point until the next time I use `cf api` to switch instances, all my CF commands will be targeted to that API endpoint.

It is also possible to see the API at which you're currently targeted by using `cf api` alone.

	PS C:\Users\bbutton> cf api
	API endpoint: https://api.beta.ironfoundry.me (API version: 2.2.0)
	
### Logging In
Once targeted at an API endpoint, you can use `cf login` to provide your username and password. There are a number of arguments you can provide to the login command, as shown below. By providing different sets of arguments, you control how many different pieces of information CF prompts you for. The only required elements are username and password. *We recommend that you never provide your password on the command line when using the login command, as that can cause your password to be exposed to others.*

	PS C:\Users\bbutton> cf help login
	NAME:
	   login - Log user in
	
	ALIAS:
	   l
	
	USAGE:
	   cf.exe login [-a API_URL] [-u USERNAME] [-p PASSWORD] [-o ORG] [-s SPACE]
	
	WARNING:
	   Providing your password as a command line option is highly discouraged
	   Your password may be visible to others and may be recorded in your shell history
	
	EXAMPLE:
	   cf.exe login (omit username and password to login interactively -- cf.exe will prompt for both)
	   cf.exe login -u name@example.com -p pa55woRD (specify username and password as arguments)
	   cf.exe login -u name@example.com -p "my password" (use quotes for passwords with a space)
	   cf.exe login -u name@example.com -p "\"password\"" (escape quotes if used in password)
	
	OPTIONS:
	   -a   API endpoint (e.g. https://api.example.com)
	   -u   Username
	   -p   Password
	   -o   Org
	   -s   Space
	
At that point, it is a simple matter to log into Iron Foundry - 

	PS C:\Users\bbutton> cf login -u ironfoundry-test@tier3.com
	API endpoint: https://api.beta.ironfoundry.me
	
	Password>
	Authenticating...
	OK
	
	Targeted org Test
	
	Select a space (or press enter to skip):
	1. qa
	2. production
	3. development
	
	Space>
	
	API endpoint: https://api.beta.ironfoundry.me (API version: 2.2.0)
	User:         ironfoundry-test@tier3.com
	Org:          Test
	Space:        No space targeted, use 'cf.exe target -s SPACE'	
In this example, we provided our username on the command line and let CF prompt us for our password. It then asked us more information about how to initalize our session by targeting the correct organization and space. We'll talk about those topics in a later article. At the end, `cf login` provided us with a summary of our current logged in state.

N.B. - If you do want to script logging in, there is another command, `cf auth` that allows you to provide all your credentials on a single line and doesn't prompt for anything else.

	PS C:\Users\bbutton> cf help auth
	NAME:
	   auth - Authenticate user non-interactively
	
	USAGE:
	   cf.exe auth USERNAME PASSWORD
	
	WARNING:
	   Providing your password as a command line option is highly discouraged
	   Your password may be visible to others and may be recorded in your shell history
	
	EXAMPLE:
	   cf.exe auth name@example.com "my password" (use quotes for passwords with a space)
	   cf.exe auth name@example.com "\"password\"" (escape quotes if used in password)
