# Scenario

Welcome to the SAP Cloud Application Programming Model hands-on session! During this session, you'll learn how to use [CAP](https://cap.cloud.sap/docs/) to build an online store, in this case, a store for books or bookstore, as we like to call it. 

So, we've established that "books" will be your product of choice for this exercise. The interesting thing about CAP is that you can easily build services, but also reuse an existing service to make your development life easier. In this case, we'll show you how to reuse a products service. 

Before you get started, it's important to understand that CAP is both [open & opinionated](https://cap.cloud.sap/docs/about/#open--opinionated). That might sound like a contradiction, but it's simple. You can choose to follow our guidance and develop along our golden path of best practices. However, you can also choose your own path, typical freestyle-style. Therefore, "open & opinionated".

Ready? Let's get started with the mission [Build a Business Application Using CAP for Java](https://developers.sap.com/mission.cap-java-app.html).

## Exercises

### [Exercise 1: Set Up SAP Business Application Studio for Development](https://developers.sap.com/tutorials/appstudio-onboarding.html)

Before you can start developing using SAP Business Application Studio, you must perform the required onboarding steps that are described in this exercise.

### [Exercise 2: Set Up SAP Business Application Studio for CAP Java](https://developers.sap.com/tutorials/cp-cap-java-app-studio.html)

First things first, you need to set up your development environment and check that everything is running smoothly.

For this exercise, we'll use the new SAP Business Application Studio as the development tool of choice. SAP Business Application Studio provides a web-based Visual Studio Code-like experience. So, it's like VS Code, but for your browser.
What's great about using SAP Business Application Studio? You get an editor, useful extensions, and all the tools required to develop CAP applications as well as full access to the terminal.

To make sure that everything is set up correctly, this exercise also includes how to build and run a simple Hello World application. 

CAP supports both Java and Node.js development. But for this exercise, we'll be using Java. The CAP Java SDK is able to tightly integrate with [Spring Boot](https://spring.io/projects/spring-boot), which provides numerous features out of the box. This means, Spring Boot will be your runtime container.

### [Exercise 3: Add a Custom Event Handler](https://developers.sap.com/tutorials/cp-cap-java-custom-handler.html)

In the following exercises, you’ll learn that the CAP Java runtime can handle all CRUD events (create, read, update, and delete) triggered by OData requests out of the box. You'll do this manually, to see how to easily write a custom event handler to extend the event handling process.

### [Exercise 4: Create a Reusable Service](https://developers.sap.com/tutorials/cp-cap-java-reusable-service.html)

The previous exercise was about quickly setting up a working CAP application and read/write some mock data. 

You’ll take advantage of all the out-of-the-box features provided by the CAP Java SDK such as using SQLite as a database for local development. As a result, you’ll remove your custom handlers written in the first exercise. In subsequent exercises, you’ll swap out SQLite with the SAP HANA service when preparing your application for the cloud.

### [Exercise 5: Reuse a CAP Java Service](https://developers.sap.com/tutorials/cp-cap-java-service-reuse.html)

Now, that your products service is ready to be reused, you’ll build a bookstore application upon it.

In this exercise, you’ll create the model and the services of the bookstore application. After that, you’ll initialize the SQLite database of your bookstore application with localized example data coming from CSV files.

You’ll then run your application – still without any custom coding required – and see the localization features of CAP in action.

### [Exercise 6: Extend the Bookstore with Custom Code](https://developers.sap.com/tutorials/cp-cap-java-custom-logic.html)

In the previous exercise, you have built the data model and exposed the services of your bookstore application. In this exercise, you’ll extend the bookstore with custom code to calculate the total and netAmount elements of the Orders and OrderItems entity. In addition, when creating an order the available stock of a book will be checked and decreased.

### [Exercise 7: Use SAP HANA as the Database for a CAP Java Application](https://developers.sap.com/tutorials/cp-cap-java-hana-db.html)

In this exercise, you’ll make the application ready to be deployed to the cloud. In order to make our application cloud-ready, we'll switch to SAP HANA as our database.

### [Exercise 8: Deploy CAP Java App to SAP Cloud Platform](https://developers.sap.com/tutorials/cp-cap-java-deploy-cf.html)

In the previous exercise, you made your application ready to run with SAP HANA. In this exercise, you'll deploy the application to the SAP Cloud Platform Cloud Foundry environment and have it running fully in the cloud.

## Support

This project is provided "as-is": there is no guarantee that raised issues will be answered or addressed in future releases.

## License

Copyright (c) 2020 SAP SE or an SAP affiliate company. All rights reserved. This project is licensed under the Apache Software License, Version 2.0 except as noted otherwise in the [LICENSE](https://github.com/SAP-samples/cloud-cap-walkthroughs/blob/main/LICENSES/Apache-2.0.txt) file.