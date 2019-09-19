# Exercise 2 - Creating a reusable Products Service

The last exercise was about quickly setting up a working CAP application. This exercise is about learning how to extend the application to a complete products service.
You'll take advantage of all the out-of-the-box features provided by the CAP Java Stack such as using SQLite as a database for local development. As a result, you'll remove your custom handlers written in the first exercise. Later, in [Exercise 5](../exercise5/README.md), you will swap out SQLite with the SAP HANA service, when preparing your application for the cloud.

## Define the Domain Model

In the last exercise you defined a service, which defined it's own entity. When modeling with CDS the best practice is to separate services from the domain model.
Therefore you will now define the complete domain model that is used by the products service. The domain model is stored in the `db` folder of your CAP application.

1. Go to your `db` folder and create a file called `schema.cds`.

    <img src="images/db_new_file.png" width="60%" />

2. Add the following code to your newly created `schema.cds` file:

    ```swift
    namespace sap.capire.products;

    using { Currency, cuid, managed, sap.common.CodeList } from '@sap/cds/common';

    entity Products : cuid, managed {
        title    : localized String(111);
        descr    : localized String(1111);
        stock    : Integer;
        price    : Decimal(9,2);
        currency : Currency;
        category : Association to Categories;
    }

    entity Categories : CodeList {
        key ID   : Integer;
        parent   : Association to Categories;
        children : Composition of many Categories on children.parent = $self;
    }
    ```

As you can see, the domain model defines two entities:
- `Products` 
- `Categories` 

It also imports various common definitions from the `@sap/cds/common` package (a globally available reuse package):
- `Currency`
- `cuid`
- `managed`
- `CodeList`

To review the imported definitions directly in your editor press and hold `CTRL`, and click on the definition.

  <img src="images/codelist_definition.png" width="100%" />

In addition the domain model uses the CDS keywords `localized`, `Association` and `Composition`.
Let's explain these imports and keywords in more detail:

### The `localized` keyword

The `localized` keyword can be used to mark elements, which require translation. The ability to store translations for different languages and to store a default fallback translation is automatically handled by the CDS model for you. You will see this in action in more detail in [Exercise 3](../exercise3/README.md).

### Associations and Compositions

Associations and Compositions can be used to define relationships between entities. They often allow you to define these relationships without explicitly working with foreign keys.
While associations define a rather loose coupling between the entities, compositions define a containment relationship. Compositions can also be thought of as defining deep structures. You can perform deep inserts and upserts along these structures.

In your domain model, the `Categories` entities define a `parent` and `children` element. This enables a hierarchy of categories. The children of a category are modelled as a composition. A category with all of its children defines a deep nested structure. Deleting a category would automatically delete all of its children. However the parent of a category is modelled as an association. Deleting a category obviously should not delete its parent.

### The `cuid` and `managed` aspects

Both `cuid` and `managed` are aspects. Aspects extend an entity with additional elements. The [`cuid`](https://cap.cloud.sap/docs/cds/common#aspect-cuid) aspect adds a `key` element `ID` of type `UUID` to the entity.

The [`managed`](https://cap.cloud.sap/docs/cds/common#aspect-managed) aspect adds four additional elements to the entity. These capture the time of the creation and last update of the entity, and the user, which performed the creation and last update.

### The `CodeList` aspect and the `Currency` type

[CodeLists](https://cap.cloud.sap/docs/cds/common#aspect-sapcommoncodelist) can be used to store global, translatable definitions based on codes, such as currencies, countries or languages. Especially for UIs, a CodeList can be useful to provide a value help for certain input fields.

The [`Currency`](https://cap.cloud.sap/docs/cds/common#type-currency) definition is a type. It defines an association to a `Currencies` entity. The [`Currencies`](https://cap.cloud.sap/docs/cds/common#entity-sapcommoncurrencies) entity is based on ISO 4217 and uses three-letter alpha codes as keys such as `EUR` or `USD` and provides the possibility to store the corresponding currency symbol such as `€` or `$`.

## Rewrite the AdminService

In [Exercise 1](../exercise1/README.md) you defined a simple service, called `AdminService`, which directly defined the entity `Products`. As you now have defined the `Products` entity in your domain model, the `AdminService` just needs to expose it. In addition, you defined the `Categories` entity, which should also be part of your service.

This can be achieved by using projections. Services expose projections of the entities defined in the domain model. These projections can be used to include only certain elements of an entity or to rename the entity's elements.
In this example you will use the most simple projection, which exposes the domain model entity without any changes.

1. Go to your `srv` folder and open the `admin-service.cds` file.

2. Replace the content with the following code:

    ```swift
    using { sap.capire.products as db } from '../db/schema';

    service AdminService {
        entity Products   as projection on db.Products;
        entity Categories as projection on db.Categories;
    }
    ```

## Deploy the domain model

Let's deploy the domain model to a database. Now, you will use SQLite, a light-weight file-based database, which fits the needs for local development perfectly. 

1. First of all install SQLite to the project.

    a. Go to the terminal where your application is running and press `CTRL + C`.   
   
    b. Run `npm install --save-dev sqlite3@^4.0.0`

2. To initialize the database with the defined domain model, run `npm run deploy`

    <img src="images/deploy_success.png" width="50%" />

    This will create a file called `sqlite.db` in your project root. The name of this database, is defined by an entry in your `package.json`.    

3. To configure your Java application to use the `sqlite.db` database file:

    a. Go to `srv/src/main/resources`, locate and open the `application.yaml` file. 
    
    This file was created when you initialized the application. 
  
    b. For the field `url` replace the string `"jdbc:sqlite::memory:"` with a reference to your local database file `"jdbc:sqlite:/home/user/projects/products-service/sqlite.db"`

    c. Set the value of `initialization-mode` from `always` to `never`, because you have already initialized the database when running `npm run deploy`.
    
    Your `application.yaml` file should look like this:
    
    ```yaml
    ---
    spring:
    profiles: default
    datasource:
        url: "jdbc:sqlite:/home/user/projects/products-service/sqlite.db"
        driver-class-name: org.sqlite.JDBC
        initialization-mode: never
    ```

## Use CAP's generic persistence handling

The CAP Java stack provides out-of-the-box capabilities to store and retrieve entities from a database. Therefore no custom coding is required for this. The entities defined in your `AdminService` will be automatically served via OData and you can just delete the `AdminService.java` file that was created earlier.

1. Delete the `AdminService.java` file in the `handlers` folder, which you have created in [Exercise 1](../exercise1/README.md). 

## Run and test your application

1. Start your application by running `mvn spring-boot:run` in the terminal and open it in a new tab.

2. Test your application by using curl from the terminal. 

    You can open additional terminals by choosing **Terminal, New Terminal** from the main menu.
    
    This request will create multiple, nested categories, at once through a deep insert:

    ```bash
    curl -X POST http://localhost:8080/odata/v4/AdminService/Categories \
    -H "Content-Type: application/json" \
    -d '{"ID": 1, "name": "TechEd", "descr": "TechEd related topics", "children": [{"ID": 10, "name": "CAP Java", "descr": "Run on Java"}, {"ID": 11, "name": "CAP Node.js", "descr": "Run on Node.js"}]}' 
    ```

3. Try to query individual categories, for example by adding the following to the end of your app URL:

    `/odata/v4/AdminService/Categories(10)`

4. Restart your application by switching to the terminal and pressing `CTRL + C` and running `mvn spring-boot:run` again. 

5. Query the categories again using the URL from step 3. You'll see that the categories are stored in a persistent database.

6. You can also expand the nested structures. Add the following to the end of your app URL:
   - `/odata/v4/AdminService/Categories?$expand=children`
   - `/odata/v4/AdminService/Categories(10)?$expand=parent`
   - `/odata/v4/AdminService/Categories(1)?$expand=children`

7. Make sure to stop your application after testing it by pressing `CTRL + C`.

## Prepare the products-service application for reuse

In [Exercise 3](../exercise3/README.md) the application will be reused by the bookstore application. The reuse of models can be achieved by publishing NPM modules with the models and defining dependencies to these NPM modules in other applications.
There are a two steps we need to perform to prepare the products-service application for reuse:

1. The name of the products-service reuse module, should be `@sap/capire-products`:
    
    a. Open the `package.json` file within the `~/projects/products-service` folder

    b. In the `name` field change the value from `products-service` to `@sap/capire-products`. If you want to you can also provide a meaningful description in the `description` field.

2. To make it easier to reuse the module an `index.cds` file can be added to the `products-service`. This ensures a better decoupling from other applications.

    a. Create a new file `index.cds` in the `~/projects/products-service` folder

    b. Place the following content inside this file:

    ```swift
    using from './db/schema';
    using from './srv/admin-service';
    ```

## Congratulate yourself on a job well done!

You have successfully developed the products service application, which is based on a CDS domain model and service definition. In [Exercise 3](../exercise3/README.md) you will build the bookstore application, reusing the products service application. You will later extend the bookstore application with custom business logic and deploy it to the cloud, using SAP HANA as the database.
