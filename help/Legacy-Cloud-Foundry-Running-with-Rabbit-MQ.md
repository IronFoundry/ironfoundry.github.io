---
layout: help_doc
title: Getting up and running with Rabbit MQ
tagline: Legacy Cloud Foundry \ Getting Started
---

# Getting up and running with Rabbit MQ

**Service Creation**

Before we start attaching to a queue in RabbitMQ, we need to create a service and bind to it.  This can be achieved by using vmc

1) Lets verify that the service is available

	vmc services
	============== System Services ==============
	+------------+------------+---------------------------------------+
	| Service | Version | Description |
	+------------+------------+---------------------------------------+
	| mongodb | 1.8 | MongoDB NoSQL store |
	| mssql | 10.50.2500 | MS SQL database service |
	| mysql | 5.1 | MySQL database service |
	| postgresql | 8.4 | PostgreSQL database service (vFabric) |
	| rabbitmq | 2.4 | RabbitMQ message queue |
	| redis | 2.2 | Redis key-value store service |
	+------------+------------+---------------------------------------+

2) Lets create a service

	vmc create-service rabbitmq redis-foobar
	Creating Service: OK
	vmc services
	=========== Provisioned Services ============
	+----------------+----------+
	| Name | Service |
	+----------------+----------+
	| redis-foobar | rabbitmq |
	+----------------+----------+

**Service Discovery, Binding and Useage**
As Step 2 above indicates, a rabbit service is ready and available to be bound to.  

Since rabbitmq uses the [AMPQ](http://www.rabbitmq.com/amqp-0-9-1-quickref.html) protocol, it is possible to reference the service from your code as an URL. For example in java you have three options:

1. use the Sprint AMPQ client

	Information about the client can be found [here](http://www.springsource.org/spring-amqp) along with some sample code.

2. Set attributes 

		ConnectionFactory factory = new ConnectionFactory();
		factory.setUsername(userName);
		factory.setPassword(password);
		factory.setVirtualHost(virtualHost);
		factory.setHost(hostName);
		factory.setPort(portNumber);
		Connection conn = factory.newConnection();

3) Use a URL 

	ConnectionFactory factory = new ConnectionFactory();
	factory.setUri("amqp://userName:password@hostName:portNumber/virtualHost");
	Connection conn = factory.newConnection();

In order to use any of the above listed information you will need to know the particulars of how the service is hosted.  This information is accessible from the System object.  To get a listing of all the environment variables:

	for (Map.Entry<String, String> envvar : System.getenv().entrySet()) {
		out.println(envvar.getKey() + ": " + envvar.getValue() );
	}

Specifically you need the following:


	VMC_RABBITMQ: xxx.xxx.xxx.xxx:yyyy


Once the application is deployed it can be bound either during the deployment "push" process or after the fact with running:

	vmc bind-service <servicename> <appname>

**Sample Application**

A very basic example:

	package wmgdispatcher;
	import com.rabbitmq.client.Channel;
	import com.rabbitmq.client.Connection;
	import com.rabbitmq.client.ConnectionFactory;
	import java.io.BufferedReader;
	import java.io.IOException;
	import java.io.InputStreamReader;
	import java.sql.SQLException;
	import java.util.logging.Level;
	import java.util.logging.Logger;

	/**
	*
	* @author sroy
	*/

	public class Wmgdispatcher {
		/**
		* @param args the command line arguments
		*/
		public static void main(String[] args) {
			// prompt the user to enter their name
			System.out.print("Enter key value: ");

			// open up standard input
			BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
			String userval = null;
			
			// read the username from the command-line; 
			try {
				userval = br.readLine();
				ConnectionFactory factory = new ConnectionFactory();
				factory.setHost("xxx.xxx.xxx.xxx");
				factory.setUsername("guest");
				factory.setPassword("guest");
				Connection connection = factory.newConnection();
				Channel channel = connection.createChannel();

				//channel.queueDeclare("FOO", false, false, false, null);
				channel.queueBind("ABCQ", "ABCEXCHANGE", "ABCQ");
				String message = "HELLOABC";
				channel.basicPublish("", "ABCQ", null, userval.getBytes());
				System.out.println(" [x] Sent '" + userval + "'");
				channel.close();
				connection.close();
			} catch (IOException ioe) {
				ioe.printStackTrace();
				System.out.println("IO error from term");
				System.exit(1);
			}
		}

	}

More advanced examples can be downloaded [here](http://support.cloudfoundry.com/entries/20322602-getting-started-with-the-rabbitmq-service-from-a-spring-application), and [here](https://github.com/rabbitmq/rabbitmq-cloudfoundry-samples/tree/master/spring). 