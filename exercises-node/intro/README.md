# Intro: All-in-one Quick Start

## Estimated time

20 minutes

## Objective

This exercise is about dipping your toes in the SAP Cloud Application Programming model ocean. We'll guide you through the initial setup for local development and the creation of your first Node.js-based project including a CDS domain model and running service. After successfully finishing this exercise, you'll have a locally-running fully-functional application ready for usage! As you'll see, CAP is ideal for both local and cloud-based development.

## Prequisites

Make sure to have the following:

 * Node.js installation with a version higher than v8.9.0
 * npm installation

## Notes
For all exercises please make sure to use **Google Chrome**.
An extended version of this exercise can be found at [Getting Started](https://cap.cloud.sap/docs/get-started/in-a-nutshell) guide of the capire page.

## Exercise description

### 1. Setup npm registry

The SAP npm registry contains all node modules developed by SAP. Setting it up is quite simple.

From the command line, run the following command:

```
npm set @sap:registry=https://npm.sap.com
```

### 2. Install cds

To install cds globally, run:

```
npm i -g @sap/cds-dk
```

   > Note: You can check your cds version, by running the following command:`cds --version`

### 3. Create a new project

To create a new CAP project, you can use the `cds init` command. This command creates the needed project configuration for you to start developing your application. Since this exercise is about creating a simple bookshop application, the project name will be **bookshop**.

To create the project, run:

```
cds init bookshop
```

After executing this command, the `bookshop` directory and needed project structure is created.

![cds init suceessful execution](./images/cds_init.png?raw=true)

### 4. Load VS Code

Now, it's time to load our IDE and access the newly created directory. 

1. From the command line, run:

    ```
    cd bookshop
    ```

2. Launch VS Code by running:

    ```
    code .
    ```

    Your CAP project is loaded directly into VS Code.

### 5. Create the domain model.

Domain models capture and conceptually define the specific entities of a domain. They usually do so in normalized ways and serve different use cases. Now we're going to create the domain model for our bookshop app.

1. Create a file called `db/schema.cds` with right click and the **New File** option as shown.

    ![create domain model](./images/create_domain_model.gif?raw=true)

    This will create a **db** directory with one file called **schema.cds**.

2. Copy the following content into the new file:

    ```swift
    namespace my.bookshop;
    using { Country, managed } from '@sap/cds/common';
    entity Books {
      key ID : Integer;
      title  : localized String;
      author : Association to Authors;
      stock  : Integer;
    }
    entity Authors {
      key ID : Integer;
      name   : String;
      books  : Association to many Books on books.author = $self;
    }
    entity Orders : managed {
      key ID  : UUID;
      book    : Association to Books;
      country : Country;
      amount  : Integer;
    }
    ```

3. Save the file.

    Our simple bookshop domain model contains three needed entities:
    - Books
    - Authors
    - Orders

    CDS ships with a pre-built model @sap/cds/common that provides common types and aspects. We use two of them:
    - the aspect `managed` 
    - the type `Country`

    More about them on the [capire page](https://cap.cloud.sap/docs/cds/common).

### 7. Create a service

In CAP, APIs are provided through services acting as facades for domain model entities. The best practice is to serve different use cases with different service facades and APIs.

Let's create our bookshop service. 

1. Create a new file called `srv/cat-service.cds`.

    Once again, this will create a new directory, this time called **srv** and a file called **cat-service.cds**.

    ![create domain model](./images/create_service.gif?raw=true)

2. Copy the following content into the new file:

    ```swift
    using my.bookshop as db from '../db/schema';
    service CatalogService {
      @readonly entity Books as projection on db.Books;
      @readonly entity Authors as projection on db.Authors;
      @insertonly entity Orders as projection on db.Orders;
    }
    ```
    The 3 entities we defined in our domain model are now exposed in our service as projections. Next, we can run our service. 

3. From the terminal, execute `cds run`.

    > If the terminal in VS Code is not open, please click on "Terminal" -> "New Terminal" from the top menu.
    ![cds run](./images/cds_run.png?raw=true)

4. The bookshop service is now up and running on http://localhost:4004. You can, for example, try to query the books entity by going to http://localhost:4004/catalog/Books. Since we have not yet added any data, you get an empty response. 

    In the next step, we will add a database and sample data.

### 8. Connect to the database and add data

Now, let’s add a database to serve some data. For this exercise, we'll keep it simple and use **SQLite**.

1. Add the SQLite driver for Node.js as a dev dependency to our project. From the terminal, run:

    ```
    npm install sqlite3 -D
    ```

2. To deploy our data model to an SQLite database, run:

    ```
    cds deploy --to sqlite
    ```
    As a result, a **sqlite.db** database file is created and the **package.json** is updated with the configuration needed for the database. Subsequent deployments can be run with `cds deploy`. You do not need to add any arguments.

    ![cds deploy](./images/cds_deploy_sqlite.png?raw=true)

3. Now let's add some data to our database.

    Add a file called **db/csv/my.bookshop-Books.csv** and copy the following content:

    ```csv
    ID;title;author_ID;stock
    201;Wuthering Heights;101;12
    207;Jane Eyre;107;11
    251;The Raven;150;333
    252;Eleonora;150;555
    271;Catweazle;170;22
    ```

4. And a file called **db/csv/my.bookshop-Authors.csv** and copy the following content:

    ```csv
    ID;name
    101;Emily Brontë
    107;Charlote Brontë
    150;Edgar Allen Poe
    170;Richard Carpenter
    ```

5. Save all files.

6. To use this data, run `cds deploy`.

    ![cds deploy](./images/cds_deploy.png?raw=true)

### 9. Run our bookshop application locally

So, now we have a connected a database and added some data. Next step is to run the **bookshop** service.

1. From the command line, run `cds run`.

2. Let's test the service again. 

    Go to http://localhost:4004/catalog/Books. You should now see the sample content added for Books in the csv file.

    ![books](./images/books.png?raw=true)

    By connecting to a fully cabable SQL database, we can leverage the querying capabilities of the generic handlers with requests like: http://localhost:4004/catalog/Authors?$expand=books($select=ID,title)

    ![authors](./images/authors.png?raw=true)

    Here we can see that the association to the books of every author is expanded.

### Congratulations!

You just learned how to set up a local development environment, developed your first CAP application and completed the Intro.

Click [here](../exercise01/README.md) to continue with Exercise 1.
