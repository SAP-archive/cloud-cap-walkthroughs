# CAA265 - Rapid Service Development with SAP Cloud Application Programming Model

Have you ever wanted to develop and run a full-fledged cloud service within minutes? Get a hands-on experience with SAP Cloud Application Programming Model, CDS, and Node.js. Keep the focus on your domain with concise yet powerful CDS data models. Expose them rapidly as OData services, write compact Node.js code to express business logic. Connect your application to SQLite and SAP S/4HANA. Benefit from accelerated development turnarounds in Visual Studio Code and the new SAP Application Studio.

## Exercises

### [Intro: All-in-one Quick Start](intro/README.md)

This intro exercise is about dipping your toes in the SAP Cloud Application Programming model ocean. We'll guide you through the initial setup for local development and the creation of your first Node.js-based project including a CDS domain model and running service. After successfully finishing this exercise, you'll have a locally-running fully-functional application ready for usage! As you'll see, CAP is ideal for both local and cloud-based development.

### [Exercise 1: Build a Modular Bookstore Application](exercise01/README.md)

In this exercise, you'll set up your development space in SAP Application Studio. With SAP Application Studio you're able to create a customized development space for creating cloud business applications with CAP. The development space comes with the needed extensions and plug-ins out-of-the-box, so you do not need to waste time installing them one by one. After getting set up, you'll create your very own CAP application, learn how to reuse published CAP packages and implement custom handlers. By the end of this exercise, you'll have a fully functional bookstore application, which users can use to browse for available books.

### [Exercise 2: Create a Reviews Service with Synchronous and Asynchronous APIs](exercise02/README.md)

In this exercise, you'll use CDS to develop a reviews service which is able to emit events. With this, your consuming application can react on changes whithout the need to trigger synchronous requests. It doesn't even need to be running when changes occur since events are safely stored in a queue. By the end of this exercise, you will have implemented actions, created events and have a service ready to be consumed by the bookstore application.

### [Exercise 3: Consume the Reviews Service from the Bookstore](exercise03/README.md)

In this exercise, the bookstore and reviews service will come together. The bookstore will consume both the asynchronous and synchronous API that the reviews service exposes. By the end of this exercise, you will have set up the bookstore and reviews service for consumption, consumed events and exposed an entity of the reviews service from the bookstore.

### [Exercise 4: Add a Fiori Elements UI for the Bookstore Application [optional]](exercise04/README.md)

In this exercise, you'll be using SAP Fiori Elements to create a UI for the catalog service that is exposed in the Bookstore application. The catalog service is exposed as an OData V4 service and we will create a List Report application on top of it, and then run it locally.

### [Exercise 5: Create an S/4 Extension with SAP Cloud Application Programming Model and SAP Cloud SDK [optional]](exercise05/README.md)

This exercise will take you to the SAP TechEd 2019 App Space mission *S/4HANA Extension with Cloud Application Programming Model*, which will show you how the SAP Cloud Application Programming Model can be used with the SAP Cloud SDK to consume a service from an SAP S/4HANA system in the context of extending core functionality with a new app and service.

Instead of consuming a service from a real SAP S/4HANA system, you’ll create and use a mock service, which mimics the equivalent service in a real SAP S/4HANA system.

## Known Issues
None

## Support

This project is provided "as-is": there is no guarantee that raised issues will be answered or addressed in future releases.

## License

Copyright (c) 2019 SAP SE or an SAP affiliate company. All rights reserved.
This project is licensed under the Apache Software License, Version 2.0 except as noted otherwise in the [LICENSE](LICENSE) file.
