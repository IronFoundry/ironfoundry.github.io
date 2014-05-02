---
layout: help_doc
title: Organizations, Spaces, and Roles
tagline: Iron Foundry V2 Beta \ Getting Started
---
# Understanding Organizations, Spaces, and Roles
Every kind of project that we work on has some sort of organizational structure to it. These structures range from departments and deployment environments in larger organizations, to indivuals and their side-projects for single-person or small-team efforts, or almost any other thing in between. The point is that structure always forms, and a good tool allows for it. The tool should allow its idea of structure to be adapted to emerging needs of its users, rather than impose a structure to follow the assumptions of the tool.

Cloud Foundry V2 has taken this advice to heart and created a flexible organizational structure representation defined through Organizations, Spaces, and Roles. These three concepts allow users of Cloud Foundry and Iron Foundry to define structures that support everything from large organizations down to single-person development shops in drawing the appropriate lines of separation between the different logic groupings in their context.

Organizations, Spaces, and Roles have a lot of influence on what users can see and do inside Cloud Foundry, so let's take a closer look at the underlying concepts.

### Organizations and Spaces
#### Organizations
At the top of the structural hierarchy are Organizations. They serve as the boundary for governance provided to all the users in that Organization along three different dimensions: quotas, service availability, and custom domains and routes. This allows a single instance of Cloud Foundry to host different Organizations representing different companies, departments, or even projects, and keep separate the resources associated with each of them. 

Organizations tend to be where managers in an organization do most their work.

#### Spaces
Beneath Organizations are its set of Spaces. Spaces define a more narrowed set of resources, scoped to a particular project, team, or environment. All application development and maintenance has to happen inside of a space. 

Spaces are where developers, QA, and operations usually are found.

### Resource Management
As described above, Organizations define governance boundaries, where resources can be limited, provided, and measured. The three main types of resources that Cloud Foundry controls are quotas, services, and custom domains and routes. 

#### Quotas
Each Organization is assigned a quota that defines the resources available to be shared across all applications. A quota is defined by a name used to identify it, the total amount of RAM that all applications together can consume, the types of services they are allowed to use (free versus premium), and the total number of routes and services that can be associated with applications in that organization. 

Here is the default quota as an example:

	Name                : default
	Max RAM             : 10G
	Non-basic services  : true
	Total routes        : 500
	Total services      : 25
	
In this case, we see that this Organization is allowed to consume up to 10G of RAM across all instances of all applications deployed, is allowed to use for-pay services and up to 25 services total, and can have up to 500 individual routes to applications. By adjusting these numbers up or down, the resources consumed, and hence the cost of operating the Organization, can be governed in one place.

The quotas can only be defined, changed, and assigned to an organization by an admin user.

#### Service Availability
Individual applications frequently need access to external services, like databases, message queues, cachces, and so on, to create web-scale offerings. Cloud Foundry makes these available to developers through the marketplace associated with each Organization. 

Individual services are installed into the marketplace by the admin user, and then made visible either to all organizations or to particular ones that are interested in using that service. Once available, developers can bind services to their applications, which make them available to be used.

	PS C:\Users\bbutton> cf marketplace
	Getting services from marketplace in org Test / space development as ironfoundry-test@tier3.com...
	OK
	
	service   plans   description
	mongodb   free    MongoDB NoSQL database
	ms-sql    free    Microsoft SQL Server Service
	
Here we see mongodb and SQL Server available in the Test Organization. Each service bound to an application counts against the Total Services allocated to an organization in its quota.

#### Custom Domains and Routes
Each application deployed to ironfoundry.me shares Iron Foundry's public domain, beta.ironfoundry.me. An application's individual URL is usually <appname>.beta.ironfoundry.me, although this can be changed through specifying an alternative host name through CF.

Developers and organnizations will likely wish to also be able to make their applications reachable through a custom URL. This is supported on Cloud Foundry through custom domains. The custom domains associated with an Organization can be viewed with `cf domains`

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

### Roles
Populating the Organizations and Spaces defined for an entity are its users, and their capabilities are defined by the roles to which they've been assigned.

The admin user has super-user capabilities in Cloud Foundry and is responsible for creating everything else in Cloud Foundry, from all users,spaces, and organizations, to all services, and beyond. The admin user is created at system creation time, directly in UAA, Cloud Foundry's OAuth2 Authentication and Authorization service. 

### New Users
When initially created through `cf create-user`, a user has no Organization or Space membership, is in no roles, and consequently can do nothing. The admin user is responsible for associating users with the appropriate Organizations and Spaces, and for giving them the right roles. 

### Using Roles
Roles define the capabilties that users have when using Cloud Foundry. There are three roles defined for each of Organization and Space users, but we'll limit ourselves to only talking about the few most frequently used roles.

#### Organizational Roles
The roles associated with Organizations mostly control administrative and managerial tasks associated with that Organization. The OrgManager role is the most important Organizational role, as they are the ones with power to affect certain things organization-wide. Some of their abilities include:

* Creating spaces
* Adding custom domains usable in any space
* Create instances of services from the marketplace

There are other tasks coming soon that the OrgManager will be empowered to do, like inviting users to an organization, but these are features that are not yet added to CF CLI.

#### Space Roles
The roles associated with particular Spaces control the tasks that users inside of those Spaces are able to do. Similar to Organizations, there is a single role that is most interesting to us, the SpaceDeveloper. The SpaceDeveloper role is used by anyone wishing to perform any action on a application or a service defined for that space. Some of their abilities include:

* Pushing an application
* Viewing information about an application
* Creating services
* Binding services to an application
* Viewing information about a service 
* Viewing logs and files

The idea is that anyone responsible for creation or operation of an application in Cloud Foundry will have the abilities they need through the SpaceDeveloper role.


