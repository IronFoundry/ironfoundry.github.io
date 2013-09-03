---
layout: help_doc
title: Provisioning Services with the Ruby VMC
tagline: Legacy Cloud Foundry \ Getting Started
---

# Provisioning Services with the Ruby VMC

First, ensure that SQL Server is available for provisioning:

	C:\cf_cli>vmc services ============== System Services ============== redis 2.2 Redis key-value store service mongodb 1.8 MongoDB NoSQL store mysql 5.1 MySQL database service neo4j 1.4 Neo4j NOSQL store mssql 10.50.2500 MS SQL database service 

Use the create-service command to provision a service for your application:

	C:\cf_cli>vmc create-service mssql mssql-myservice C:\config_cli>vmc services ============== System Services ============== redis 2.2 Redis key-value store service mongodb 1.8 MongoDB NoSQL store mysql 5.1 MySQL database service neo4j 1.4 Neo4j NOSQL store mssql 10.50.2500 MS SQL database service =========== Provisioned Services ============ mssql-myservice mssql 

Finally, bind the new service to your ASP.NET application:


	C:\cf_cli>vmc bind-service mssql-myservice testwebapp C:\cf_cli>vmc apps App name: testwebapp Instances: 1 State: STARTED Services: mssql-myservice 

When bound to an ASP.NET application, a provisioned SQL Server database will be set as the "Default" connection string in the application'sWeb.config file:

	<connectionStrings> <add connectionString="server=10.80.71.38,1433;uid=uLqXk1J8cgMq4;pwd=pOmfdCSgG5qEQ;trusted_connection=false;" name="Default" /> </connectionStrings> 

Here is an example of creating and binding a Mongo DB service:

	C:\cf_cli>vmc services ============== System Services ============== redis 2.2 Redis key-value store service mongodb 1.8 MongoDB NoSQL store mysql 5.1 MySQL database service neo4j 1.4 Neo4j NOSQL store mssql 10.50.2500 MS SQL database service =========== Provisioned Services ============ mssql-myservice mssql C:\cf_cli>vmc create-service mongodb mongodb-myservice C:\cf_cli>vmc services ============== System Services ============== redis 2.2 Redis key-value store service mongodb 1.8 MongoDB NoSQL store mysql 5.1 MySQL database service neo4j 1.4 Neo4j NOSQL store mssql 10.50.2500 MS SQL database service =========== Provisioned Services ============ mongodb-myservice mongodb mssql-myservice mssql C:\cf_cli>vmc bind-service mongodb-myservice testwebapp C:\cf_cli>vmc apps App name: testwebapp Instances: 1 State: STARTED Services: mssql-myservice, mongodb-myservice 

The service credentials are available in the Web.config file's <appSettings />. The key is VCAP_SERVICES and the value is the JSON corresponding to the bound services' credentials:

	"mssql-10.50.2500": [ { "name": "mssql-myservice", "label": "mssql-10.50.2500", "plan": "free", "tags": [ "mssql", "SQL Server 2008 R2", "relational" ], "credentials": { "name": "d208c0247b8fa4fa894366a45505e5387", "hostname": "10.80.71.38", "host": "10.80.71.38", "user": "uLqXk1J8cgMq4", "username": "uLqXk1J8cgMq4", "password": "pOmfdCSgG5qEQ" } } ], "mongodb-1.8": [ { "name": "mongodb-myservice", "label": "mongodb-1.8", "plan": "free", "tags": [ "mongodb", "mongodb-1.8", "nosql" ], "credentials": { "hostname": "127.0.0.1", "host": "127.0.0.1", "port": 25001, "username": "2b244604-e3ff-40f9-881f-c06fcddc7a49", "password": "48060484-14c5-4325-b5c9-5db0fcb946ac", "name": "effb0a0c-a213-4586-9cd9-01a7a8f9b5f5", "db": "db" } } ]