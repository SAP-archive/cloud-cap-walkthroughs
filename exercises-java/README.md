# Scenario

Welcome to the SAP Cloud Application Programming Model hands-on session! Wow... that's a mouthful. From now on, let's just call it CAP hands-on. During this session, you'll learn how to use [CAP](https://cap.cloud.sap/docs/) to build an online store, in this case, a store for books or bookstore, as we like to call it. 
So, we've established that "books" will be your product of choice for this exercise. The interesting thing about CAP, is that you can easily build services, but also reuse an existing service to make your development life easier. In this case, we'll show you how to reuse a products service. 
Before you get started, it's important to understand that CAP is both [open & opinionated](https://cap.cloud.sap/docs/about/#open--opinionated). That might sound like a contradiction, but it's really quite simple. You can choose to follow our guidance and develop along our golden path of best practices. However, you can also choose your own path, typical freestyle-style. Therefore, "open & opinionated".
Ready? Let's get started...

## Excercises

### [Exercise 1: Getting started: Development environment and Hello World](exercise1/README.md)

First things first, you need to set up your development environment and check that everything is running smoothly.

For this exercise, we'll use the new SAP Application Studio as the development tool of choice. SAP Application Studio provides a web-based Visual Studio Code-like experience. So it's like VS Code, but for your browser.
What's great about using SAP Application Studio? You get an editor, useful extensions and all the tools required to develop CAP applications as well as full access to the terminal.

To make sure everything is set up correctly, this exercise also includes how to build & run a simple Hello World application. 
CAP supports both Java and Node.js development. But for this exercise, we'll be using Java. The CAP Java SDK is able to tightly integrate with [Spring Boot](https://spring.io/projects/spring-boot), which provides a lot of features out of the box. This means, Spring Boot will be your runtime container.

### [Exercise 2: Creating a reusable Products Service](exercise2/README.md)

The last exercise was about quickly setting up a working CAP application. This exercise is about learning how to extend the application and to build a complete products service. You'll take advantage of all the out-of-the-box features provided by the CAP Java SDK. As a result, you'll remove your custom handlers and use SQLite as a database for local development. Later, in Exercise 5, you will swap out SQLite with the SAP HANA service, when preparing your application for the cloud.

### [Exercise 3: Building the Bookstore](exercise3/README.md)

Now that your products service is ready to be reused, you will build your bookstore application. In this exercise you will create the model and the services of the bookstore application. 
After that you will initialize the SQLite database of your bookstore application with localized example data coming from CSV files. 
You will then run your application - still without any custom coding required - and see the localization features of CAP in action.

### [Exercise 4: Extending the Bookstore with custom code](exercise4/README.md)

In the last exercise you built the data model and exposed the services of your bookstore application. In this exercise you will extend the bookstore with custom code to calculate the `total` and `netAmount` elements of the `Orders` and `OrderItems` entity. In addition when creating an order the available stock of a book will be checked and decreased.

### [Exercise 5: Using SAP HANA as database](exercise5/README.md)

In this exercises you will make the application ready to be deployed to the cloud. In order to make our application cloud-ready, we'll switch to SAP HANA as our database.

### [Exercise 6: Deploying to the cloud](exercise6/README.md)

In the last exercise you made your application ready to run with SAP HANA. In this exercise you'll deploy the application to the SAP Cloud Platform Cloud Foundry environment and have it running fully in the cloud.
