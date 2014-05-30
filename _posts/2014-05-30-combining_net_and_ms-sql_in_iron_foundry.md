---
layout: post
title: Combining .NET and MS-SQL in Iron Foundry
categories:
- .NET
- Iron Foundry
- Cloud Foundry
tags: []
status: publish
type: post
published: true
author: Brian Button
twitter: brianbuttonxp

---

In this article, I'll show a simple ASP.Net application that uses a SQL-Server database for data access. We'll talk about how to create your database, and about how to bind the database service to the application. These are usually very simple tasks, but certain requirements of Cloud Foundry and Iron Foundry make it a little more complicated. 

If you don't understand what service brokers are in Cloud Foundry, please take a minute and [read up on it](/help/how_services_and_service-brokers_are_used_in_cloud_foundry.html). The concept is important through the rest of this article. 

### Building our Application
The application described here is really simple. It is a standard ASP.Net MVC application, only slightly modified from the standard example app created by Visual Studio.NET. We'll assume the ASP.Net code as a given and only talk about the interesting changes. The code for this application is available through [github](https://github.com/ironfoundry/if_sample_apps), in the MsSQL-Binding-Sample folder.

#### Creating the database model
Creating a database model is usually very easy. It's a little more complicated in Cloud Foundry because you don't have direct access to the database server. Services that run inside Cloud Foundry exist on one or more service VMs on Cloud Foundry's internal network. This prevents you from directly attaching to the database server with SQL Server Manager. 

There are a couple of ways that we can get around this. The first is by creating firewall rules that would directly expose the SQL Server instance to the public internet. Based on our judgement and experience with exposing anything to the raw internet, we chose not to do this. The way that we did choose is to let your application create the database itself and seed it with the appropriate data at startup. This technique is described fully [here](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application). What follows is how we used Entity Framework Code First in our sample application.

#####Creating the entity classes#####
The first step is to define our entity classes. These are basically Plain Old C# Objects (POCO) almost. There were a couple of concessions we had to make in order to create relationships between them and establish primary keys. Here are the two classes:

	namespace SoftballStatsViewer.Models
	{
	    public class Player
	    {
	        public int ID { get; set; }
	        public string PlayerName { get; set; }
	        public string Position { get; set; }
	        public int TeamId { get; set; }
	
	        public virtual Team Team { get; set; }
	    }
	
	    public class Team
	    {
	        public Team()
	        {
	            Players = new List<Player>();
	        }
	
	        public int ID { get; set; }
	        public string SchoolName { get; set; }
	        public string Nickname { get; set; }
	
	        public virtual ICollection<Player> Players { get; set; }
	    }
	}

In both of these classes, we had to add an ID property to represent the primary key. As an alternative, we could have added an attribute on a different field to make it the primary key, but that forces a dependency on the Entity Framework for classes that otherwise don't need it. We could also have manually told the Entity Framework the name of our primary key property in a different way, but that was overly complex for this example.

We also had to add a virtual property, _Players_, in Team to model the list of players that a team has. This allows the Entity Framework to populate the Players collection inside Team at runtime. Similarly, we added a _Team_ virtual property in Player to provide a back reference to the team a player plays for. 

So, these classes are close to POCOs, but with minor concessions.

#####Building the database context class#####
Once the entity classes are built, we need to construct the database context that describes the classes to the Entity Framework:

	namespace SoftballStatsViewer.Models
	{
	    public class TeamContext : DbContext
	    {
	        public TeamContext() : base("TeamContext")
	        {
	        }
	
	        public DbSet<Team> Teams { get; set; }
	        public DbSet<Player> Players { get; set; }
	
	        protected override void OnModelCreating(DbModelBuilder modelBuilder)
	        {
	            modelBuilder.Conventions.Remove<PluralizingTableNameConvention>();
	        }
	    }
	}

Here, we provide a standard way to access the collections of Players and Teams, as well as customize how the Entity Framework names the tables created from our entities. In this class, we could also have manually described the relationships between our tables, defined what our primary keys were called, and specified any foreign keys we had. To keep things simple, we kept the code as described previously. 

#####Initializing our database#####
Entity Framework provides a way to seed data into a database through initializers. The specific behavior of initializers is controlled by their base class. There are several different choices for these base classes, each for a different purpose:

* CreateDatabaseIfNotExists<TDbContext> - creates the database schema if no database existed previously,
* DropCreateDatabaseAlways<TDbContext> - always drops and recreates the database,
* DropCreateDatabaseIfModelChanges<TDbContext> - only drops and recreates the database if the underlying entity model has changed.

Of these three, the last one seems to be the most useful, especially during development. This way our database would stay current as our entity model changed, which would prevent errors from schema mismatches. When we deployed, however, this should be changed to prevent dropping and recreating the prodution database. 

Fortunately for us, dropping the production database is impossible because of the way our MS-SQL service broker works. Our service broker uses a feature of SQL Server 2012 called Contained Databases. A contained database is one that is isolated from other databases and from the instance of SQL Server on which it is hosted. This was chosen because it provided the greatest amount of segregation between databases provisioned for different users, and also isolated users from having any access to the master database. 

When deployed to Cloud Foundry, using _DropCreateDatabaseIfModelChanges_ as the base class was failing every time. It turns out that you need access to the master database to drop your own database, and we explicitly deny access to master. Therefore, you can't drop any databases through our service broker. So the only way we could make this to work was to change to _CreateDatabaseIfNotExists_ for production deployment. It makes it a little more complicated to move from development to production, since this code change has to happen, but it is worth doing for the convenience in development.

Here is the code for our initializer:

	namespace SoftballStatsViewer.Models
	{
	    public class TeamInitializer : CreateDatabaseIfNotExists<TeamContext>
	    {
	        protected override void Seed(TeamContext context)
	        {
	            var players = new List<Player>
	            {
	                new Player{ ID = 5, PlayerName = "Linsey", TeamId = 5},
	                new Player{ ID = 6, PlayerName = "Jane", TeamId = 5}
	            };
	            players.ForEach(p => context.Players.Add(p));
	
	            var team = new Team { SchoolName = "DePauw", Nickname = "Tigers", ID = 5 };
	            var teams = new List<Team>
	            {
	                team
	            };
	
	            teams.ForEach(t => context.Teams.Add(t));
	            context.SaveChanges();
	        }
	    }
	}

#####Setting up our web.config file#####
There were a few simple additions needed to our web config. 

We needed to add a connection string for use during development. This was just a standard connection string without anything special added to it:

	  <connectionStrings>
	    <add name="TeamContext" connectionString="Data Source=(LocalDb)\v11.0;Initial Catalog=TeamsDB;Integrated Security=SSPI;" providerName="System.Data.SqlClient" />
	  </connectionStrings>
	 
This connection string is very important in the binding process for a database service, and we'll discuss why at length shortly.

And in the EntityFramework configuration section, we had to define the TeamInitializer as the initializer to use when seeding data:

    <contexts>
      <context type="SoftballStatsViewer.Models.TeamContext, SoftballStatsViewer">
        <databaseInitializer type="SoftballStatsViewer.Models.TeamInitializer, SoftballStatsViewer" />
      </context>
    </contexts>
    
####Deploying to Cloud Foundry####
Finally, we're ready to deploy the application to Cloud Foundry and Iron Foundry. In addition to pushing our application, this also involves binding an existing service broker instance to our application and directing our connection string to the service-broker database instance. After that, things should just work. But, as with many things, its not quite that simple...

#####Binding to the service#####
It's not quite as simple as it might be because the service broker allocates a new database instance, userid, and password each time a service is bound to your application. And there is no way to know what any of that information is until you bind to the service. Fortunately, binding to your application is a permanent relationship that will exist through multiple updates, until such time as you delete your application or unbind the service.

There are several  ways to bind your application to a service, and we'll describe them next. Each of these assume that the service broker is already is already created and available to be bound in your Space in Cloud Foundry.

___Completely manually___
This is the completely manual version, so that you can see what the individual steps are. 

* Push your application using `cf push app_name -s windows2012 --no-start`. There is no need to start the application, because presumably it won't work without its database.
* Bind the service to it explicitly using `cf bind-service app_name service_name`.
* Re-push your application to allow the binding operation to take effect. This is required by Cloud Foundry, since it has to set environment variables that have to be available to your application. The application is still not ready to run yet since the connection string hasn't been changed to point to the hosted MS-SQL yet.
* Change the connection string for the database in your web.config to match the connection string in the VCAP_SERVICES environment variable. You can get the VCAP_SERVICES variable from Cloud Foundry using `cf files app_name logs/env.log`. Find VCAP_SERVICES in that file, copy out your connection string, edit your local web.config, then re-push your application. Now it should work!

As I said, this is the completely manual way, just to illustrate the discrete steps involved. We can optimize this, however, to make the process easier.

___Programmatically binding___
To prevent the third push, it is possible to programmatically read the VCAP_SERVICES variable from the runtime after the second push. There is an example of doing this, along with a convenience class called _CloudFoundryConnectionStringBinder_, in the MsSQL-Binder-Sample on [github](https://github.com/ironfoundry/if_sample_apps).

To make use of this, every time your code needs to access the connection string, it can call _CloudFoundryConnectionStringBinder.Bind()_, which will programmatically determine the right connection string contents for your environment. If you are still in development, for example, it will return the string from your web.config but will return the correct value for your hosted MS-SQL instance if running on Cloud Foundry. 

_The one trick to making this work is that you'll need to make the connection string name in web.config match the service name on Cloud Foundry. Assuming they match, the Bind method will be able to return the correct connection string to you._

You'll still need to follow the first three steps above to get things working, but we did cut out the manual edit of your config file and the last push.

___Using a Manifest to Bind___
The final way is the best and most convenient. It can be done with a single push by using the convenience class as described above, and by creating a  manifest file for your application that specifies the services used. When pushing your application, Cloud Foundry will automatically bind to those services for you on your first push. Here is a sample manifest, the important part being the bit at the end:

	---
	applications:
	- name: SoftballStats
	  memory: 512M
	  instances: 1
	  services:
	  - free-sql

As long as the service name in the manifest exists in your Space on Cloud Foundry, and you have a connection string name matching that service name in your web.config, the binding should work on your first push. That's the simplest way for you to bind your application.

###Conclusion###
Thanks for sticking with this whole blog entry. I know it covered a lot of territory, from how to create an application that creates its own database, to a discussion of why that is necessary with the current version of Cloud Foundry, to finally talking about the mechanics of how to bind a service to your application. 

Hopefully you found this information useful and interesting. If so, please help us out by tweeting about it, posting it to your favorite social media sites, or however else you can help us get a few more eyes on this! 
