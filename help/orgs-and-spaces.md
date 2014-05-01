---
layout: help_doc
title: Organizations and Spaces
tagline: Iron Foundry V2 Beta \ Getting Started
---
# Understanding Organizations, Spaces, and Users
Every kind of project that we work on, including single-person efforts, has some sort of organizational structure to it. That may be departments and deployment environments in larger organizations, indivuals and their side-projects for single-person or small-team efforts, or almost any other thing in between. The point is that structure always forms, and a good tool allows for it. The tool should allow its idea of structure to be adapted to emerging needs of its users, rather than force that structure to follow the assumptions of the tool.

Cloud Foundry V2 has taken this advice to heart and created a flexible organizational structure representation defined through Organizations and Spaces. These two concepts allow users of Cloud Foundry and Iron Foundry to define structures that support everything from large organizations down to single-person development shops, in drawing the appropriate lines of separation between the different logic groupings in their context.

These Organizations and Spaces have a lot of influence on what users can see and do inside Iron Foundry, so let's take a closer look at the underlying concepts.

### Organizations and Spaces
#### Organizations
At the top of the structural hierarchy are Organizations. They serve as the boundary for governance provided to all the users in that organization along three different dimensions: quotas, service availability, and custom domains and routes. This allows a single instance of Iron Foundry to host different Organizations representing different companies, departments, or even projects, and keep the resources associated with each of them separate. 

Organizations tend to be where managers in an organization do most their work.

#### Spaces
Beneath Organizations are its set of Spaces. Spaces define a more narrowed set of resources, scoped to a particular project team or environment. All application development and maintenance has to happen inside of a space. 

Spaces are where developers, QA, and operations usually are found.

### Resource Management
As described above, Organizations define governance boundaries, where resources can be limited, provided, and measured. The three main types of resources that Iron Foundry controls are quotas, services, and custom domains and routes. 

#### Quotas
Each Organization is assigned a quota that defines the resources available to be shared across all applications in the Organization. A quota is defined by a name used to identify it, the maximum amount of RAM that all applications together can consume, the types of services they are allowed to use (free versus premium), and the total number of routes and services that can be associated with applications in that organization. 

Here is the default quota as an example:

	Name                : default
	Max RAM             : 10G
	Non-basic services  : true
	Total routes        : 500
	Total services      : 25
	
In this case, we see that this Organization is allowed to consume up to 10G of RAM across all instances of all applications deployed, is allowed to use for-pay services and up to 25 services total, and can have up to 500 individual routes to applications. By adjusting these numbers up or down, the resources consumed, and hence the cost of operating the Organization, can be governed in one place.

The quotas can only be defined, changed, and assigned to an organization by an admin user.

#### Service Availability
Individual applications frequently need access to external services, like databases, message queues, cachces, and so on, to create web-scale offerings. Iron Foundry makes these available to developers through the marketplace associated with each Organization. 

Individual services are installed into the marketplace by the admin user, and then made visible either to all organizations or to particular ones that are interested in using that service. Once available, developers can bind services to their applications, which make them available to be used.

	PS C:\Users\bbutton> cf marketplace
	Getting services from marketplace in org Test / space development as ironfoundry-test@tier3.com...
	OK
	
	service   plans   description
	mongodb   free    MongoDB NoSQL database
	ms-sql    free    Microsoft SQL Server Service
	
Here we see mongodb and SQL Server available in the Test Organization. Each service bound to an application counts against the Total Services allocated to an organization in its quota.

#### Custom Domains and Routes
Each application deployed to Iron Foundry shares Iron Foundry's public domain, beta.ironfoundry.me. An application's individual URL is usually <appname>.beta.ironfoundry.me, although this can be changed through specifying an alternative host name through CF.

Developers and organnizations will likely wish to also be able to make their applications reachable through a custom URL. This is supported on Iron Foundry through custom domains. The custom domains associated with an Organization can be viewed with `cf domains`

	PS C:\Users\bbutton> cf domains
	Getting domains in org Test as ironfoundry-test@tier3.com...
	name                                 status
	beta.ironfoundry.me                  shared
	agileprogrammer.net                  owned

When needed, additional custom domains can be associated with an Organization using `cf create-domain`.

	PS C:\Users\bbutton> cf create-domain Test if-test.org
	Creating domain if-test.org for org Test as ironfoundry-test@tier3.com...
	OK
	
	PS C:\Users\bbutton> cf domains
	Getting domains in org Test as ironfoundry-test@tier3.com...
	name                  status
	beta.ironfoundry.me   shared
	agileprogrammer.net   owned
	if-test.org           owned
	
Once the domain is added to an Organization, it can be made publicly available through adding a DNS CNAME record pointing to it.