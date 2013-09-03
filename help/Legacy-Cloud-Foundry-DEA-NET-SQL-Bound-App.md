---
layout: help_doc
title: How is SQLServer bound to an app?
tagline: Legacy Cloud Foundry \ DEA .NET (Droplet Execution Agent)
---

# How is SQLServer bound to an app?

When you bind an app to an SQL Server, the DEA modifies the "Default" connection string to have the correct settings, as in this example:

	<connectionStrings>
		<add name="Default" connectionString="Data Source=10.0.0.1;Initial Catalog=dd972ce4bdd0c4a64b8aaf492153b6822;Integrated Security=False;User ID=u9LlGd78hpOIy;Password=pXlUPPzkRCliL;Connect Timeout=30" />
	</connectionStrings>

All you need to do as an application developer is reference this connection string in code to use it:

	string connString = WebConfigurationManager.ConnectionStrings["Default"].ConnectionString;