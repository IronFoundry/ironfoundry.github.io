![Thor](http://adronhall.smugmug.com/Software/Software-Development/Pyrocumulus/i-NqSGc4m/0/S/Marvel-vs-Capcom-3-MVC3-S.jpg "Thor")
Project Thor Overview
===
The Thor Project is setup to deliver a high quality, solid user experience, and resilient user interface for Cloud Foundry (w/ Iron Foundry Extension Support) PaaS enabled systems to the Apple OS-X System. This project, to ensure a solid user experience utilizes the Cocoa Framework.

_**Please fork and contribute back.**_
License
---
Copyright 2012 Iron Foundry Organization

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

[http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

   Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.

**Getting the Code**

To clone/fork/download the latest code to work with, contribute, and send pull requests with follow these steps.

 1. Navigate to the main source (where you probably already are since you're reading this document) and fork the code. [Thor Source Code](https://github.com/IronFoundry/Thor)
 2. Once you've forked the code, navigate to your repository and clone to your local development machine.

`https://github.com/IronFoundry/Thor.git`

 3. Once the clone is complete, pull the external references using [CocoaPods](http://cocoapods.org).

`pod Intall`

Your local repository should have executable code now. Open the project with XCode and see if everything works. If it doesn't, please post a comment to the issues list.

**Working on the Code**

Once you've added the feature, or completed one of the stories or items in the [Issues List](https://github.com/IronFoundry/Thor/issues?state=open) leave a comment on the issue and submit a pull request (or just submit the pull request). I'll then merge it back in, or if there are conflicts we work with you to merge it back in and add the code to the master branch.


#Getting Started#

##Adding a New Cloud Connection##
When you start Thor you will see the following screen:  
![Thor1](https://raw.github.com/IronFoundry/Thor/master/images/Thor1.png)

This will let you either add a new application or cloud connection. Typically you will want to add a new connection to a cloud account. You can click the add button and then 'New Cloud...'. You will be presented with the following sheet to enter in your information:  
![Thor2](https://raw.github.com/IronFoundry/Thor/master/images/Thor2.png)

The common case is that url will be http://api.ironfoundry.me.

Enter the email address and password credentials that were mailed to you upon signup and click OK. You will see a cloud icon show up in your clouds list.  
![Thor3](https://raw.github.com/IronFoundry/Thor/master/images/Thor3.png)  

When you select your cloud connection you will see all the applications that you have pushed and the services that you have assigned to your cloud.  
![Thor4](https://raw.github.com/IronFoundry/Thor/master/images/Thor4.png)  

##Adding a New Application##
Adding a new application allows you to take a local application from your file system and prepare it for upload to a cloud connection. Adding a new application is similar to adding a cloud connection. You click the add button and you will presented with a finder window. Choose the folder with your application and click open. Once you have an application it will be added to local applications:  
![Thor5](https://raw.github.com/IronFoundry/Thor/master/images/Thor5.png)  

##Deploying an Application##
To create a new deployment for your application, you click new deployment. You will be presented with the following sheet to choose the cloud to deploy:  
![Thor6](https://raw.github.com/IronFoundry/Thor/master/images/Thor6.png)  

Once you choose the cloud to deploy it will present you with the following sheet to create a name, memory and number of instances for your app (the name will be the first part of your uri so choose wisely):  
![Thor7](https://raw.github.com/IronFoundry/Thor/master/images/Thor7.png)  

Once you have made the choices for you application the local application will be bound to a cloud connection. You can then push the application to deploy it to the cloud. Anytime you make changes to your local application, you can push those changes by pushing it again. You can always associate the same application to multiple cloud connections.    
![Thor8](https://raw.github.com/IronFoundry/Thor/master/images/Thor8.png)  

##Managing Services for your Cloud Connection##
You can add services associated to your cloud connection that will be available to your applications.
![Thor9](https://raw.github.com/IronFoundry/Thor/master/images/Thor9.png)  

When you add a new service you will be presented with the following sheet containing the available services:  
![Thor10](https://raw.github.com/IronFoundry/Thor/master/images/Thor10.png)  

This will show up in your services. You can also remove services by clicking the remove (-) button by a service.

##Monitoring an Application##
You can monitor your application by clicking on your application from the cloud connection:  
![Thor11](https://raw.github.com/IronFoundry/Thor/master/images/Thor11.png)  

Here you can see your instances and their status. You can stop / start / restart your application. You can also edit the settings of your application to add more instances / memory.

When you bind a service you will be presented with a list of services associated with your cloud connection:  
![Thor12](https://raw.github.com/IronFoundry/Thor/master/images/Thor12.png)  

Once you bind your service you will see it associated with your application:  
![Thor13](https://raw.github.com/IronFoundry/Thor/master/images/Thor13.png)  

