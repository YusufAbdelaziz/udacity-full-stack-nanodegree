# Creating an API with PostgreSQL and Express

## Lesson 1 : Introduction.

- Goals
    - Create a RESTful Node API with Express
    - Write SQL queries for Postgres to power an API
    - Design a clean Node API with well organized logic, full test coverage, and database management through migrations
- Course Topics
    - Different kinds of databases and what they're for
    - Relational Database structure, queries, and common commands
    - Relational Database joins
    - Database migrations
    - CRUD for Node models
    - REST structure for Express Endpoints
    - CORS enabled API
    - API Testing
    - Password hashing for security
    - JWT's for authentication and protected endpoints
- Course Outline
    
    ### **Databases and SQL**
    
    - Gain a general understanding of databases, their purpose and use cases for different types and structures. This course uses Postgres, a relational database, so we will spend the majority of the lesson learning more about Postgres and experimenting with some of the most common and useful SQL commands and concepts.
    
    ### **API with Postgres**
    
    - Learn all the ins and outs of creating a Node API backed by a Postgres database. This lesson includes concepts and practices you are likely to use every day in a web development or software engineering job, such as **database migrations**, **environment variables**, and **integration testing**,
    
    ### **REST API with Express**
    
    - To complete the API, we turn our focus to the client-facing Express logic. We will cover what it means to create a RESTful API and you will learn good practices for clean code architecture in a Node application. We also touch on important concepts like CORS and Express middleware.
    
    ### **Authentication and Security in a Node API**
    
    - **Password hashing**, **salt and pepper**, **JWTs**, and more - this lesson is all about data security and authentication. You will be introduced to the best industry standard libraries for these security measures and pick up some good habits along the way.
    
    ### **SQL for advanced API functionality**
    
    - In the last lesson we pick up right where we left off with SQL and learn queries and database concepts to extend our API in powerful ways. We cover joins and database relationships, and use them to create new concepts in our API like cart functionality and how to create dashboard endpoints filled with useful information.
- What is an API ?
    - Stands for Application Programming Interface.
    - It’s an interface through which we interact with data in a database (in case of backend context).
    - API is designed to supply programs with data (mobile app, websites, etc.).
    - An endpoint is similar to a page or a route in a website. It’s used to get straight data.
    - Some businesses build an API as a service which means that their data are the product and they make them available by a program which can be accessed via an SDK.
    - API can also be thought as the interface we use to utilize a library or other program. So it might be the set of methods/variables that other developers has made available for you to use.

## Lesson 2 : Databases and SQL.

- What is a database ?
    - A database is a large collection of data organized especially for rapid search and retrieval.
- SQL/Relational Databases
    - In this type, SQL type databases are organized to be query-able using SQL and organize data in spreadsheet or tables. An item is stored in a row in database, and each item’s properties are represented by columns.
    - Relational databases are really useful when we want a structured data and have multiple tables with which each one is connected via a relation.
    - Typical use cases include : user info, product inventories, and blogs.
    
    ### Common RDBMS (Relational Database Management System)
    
    - MySQL.
    - PostgreSQL.
    - MariaDB.
    - MSSQL server
- NoSQL/Non-relational databases.
    - In NoSQL DBs, you store data in various forms than tables. You also don’t use SQL to make some queries on the data.
    - Use cases include : partially structure or unstructured data which may be a really big collection of complex data or caches.
    
    ### Types of NoSQL DBs.
    
    - **Key-Value store** → This kind of NoSQL database is fast because you store data in a key-value pair (built upon hash tables) such that the key is unique and you can store any kind of data you want. ***Redis*** DB is an example for this type.
    - **Document store** → Data are stored in documents. The data might be unstructured or arbitrarily nested which can be a headache to account for in a relational way. ***MongoDB*** and ***Elasticsearch*** are examples for this type.
    - **Column-Oriented** → Data are organized into columns instead of rows. This architecture scales pretty well and makes efficient queries. Note that this DBMS can be used with SQL. ***Apache Cassandra*** is an example for this type.
- Why Postgres is used in this course ?
    - **Availability** → It’s open source, and hence can be used with any project.
    - **Common** → RDBMS are most common type of DBs nowadays.
    - **Popular and well tested** → Postgres is a popular choice for enterprise software.
    - **Transferable skills** → Since Postgres uses SQL, the amount of skills gained while learning Postgres can be transferable to other SQL DBs like MySQL and other RDBMS.
    
- What is SQL ?
    - SQL stands for Structured Query Language and it’s a language or syntax used to interact with SQL type databases so it’s obviously not a database per se.
    - In other words, it’s a language to interact with RDBMS.
- How to start psql prompt ?
    - You can type *`psql -U <username>`* at the PowerShell (remember to add the bin folder of postgres in the variables environment so the command would be recognized).
    - Our user name would be `postgres`.
- How to create a new database?
    - You can use the following command :
        
        ```sql
        CREATE DATABASE my_new_db;
        ```
        
    - Quick notes :
        - Your db name should be lowercase and separated with underscores.
        - Each SQL command should be written in uppercase (it doesn’t matter but it’s a convention) and should end with a semicolon. Forgetting to do so would result in a new line that waits for the remaining of the previous command.
- How to connect to a database ? and what is meta commands ?
    - You can connect to a database using :
        
        ```sql
        \c my_db;
        ```
        
    - [Meta commands](https://dataschool.com/learn-sql/meta-commands-in-psql/) are system-level commands that helps you to navigate, manage, and view different databases.
- How to quit PostgreSQL and how to directly run PostgreSQL on a certain DB ?
    - To quit, you can type `\q`
    - To directly connect to a certain DB type →
        
        ```sql
        psql -U postgres plants_dev
        ```
        
    
- How to create a table ?
    - You can create a table using the following command :
        
        ```sql
        CREATE TABLE table_name (column_name1 column_type, column_name2 column_type);
        ```
        
- Some data types in Postgres.
    - You can use VARCHAR for a variable-length string. If you didn’t specify the number of characters, the default is 255 character.
    - “text” can be used to represent long texts.
    - “integer” can be used for a signed four-byte integer data.
    - “date” can be used to store date data.
    - For more info about data types in Postgres, click [here](https://www.postgresql.org/docs/current/datatype.html).
    
- How to display the tables exist in a database? How to display all databases in a system?
    - You can use `\dt` meta command which stands for “display tables”.
    - You can use `\l` or `\list` to display all databases you have in your system.
- What is a schema ?
    - Schema describes structure of the database. So the columns and column types of each table in the database can be abbreviated as schema.
    - To define a schema, you can create an [ERD](https://www.lucidchart.com/pages/er-diagrams) (Entity Relationship Diagram).
- How id column is useful ? and how to create an autoincremented id column ?
    - ID column is primarily used to distinguish each row which helps in retrieving that row easily.
    - You can create an auto-incremented id column using the following data types →
        
        ```sql
        CREATE TABLE my_table (id SERIAL PRIMARY KEY, other columns );
        ```
        
    - SERIAL is an autoincrementing four-byte integer data type.
    - PRIMARY KEY implies that this column should be provided and cannot be null.
    
- Cheat Sheet and Tips.
    
    ### **Tips and Tricks**
    
    - Remember you can get out of pqsl with `\q`
    - Database names should use underscores
    
    ### **SQL Cheat Sheet**
    
    ### **Meta Commands**
    
    - `\l` **List** databases
    - `\c` **Connect** to a database
    - `\dt` **Display Tables** in a database
    - `\q` **Quit** out of psql to normal terminal
    
    ### **Queries**
    
    - `CREATE DATABASE database_for_all_things`
    - `CREATE TABLE first_things (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50),
    count integer
    );`
- What are CRUD operations ?
    - CRUD stands for Create, Read, Update, and Delete.
- How to create a new entry (row) in a table ?
    - You can use the `INSERT` command as follows :
        
        ```sql
        INSERT INTO table_name (columns) VALUES ()
        ```
        
    - Notice that columns order must be the same as the order of values inserted. Also, you don’t need to specify the “id” column because it’s autoincremented
    - An example →
        
        ```sql
        INSERT INTO plants (name, description, individuals, sighting_date) VALUES('Dandelion', 'Fuzz yellow shit', 5, '2022-8-31');
        ```
        
    
- How to read data from a table ?
    - You can use `SELECT` command as follows.
        
        ```sql
        SELECT * FROM table_name;
        ```
        
    - Notice that the asterisk brings all columns that is related to the row. Also, to make a particular search depending on a column’s value, you can use the `WHERE` clause but we’d discuss it later.
    
- How to update a specific row ?
    - You can use the UPDATE command as follows in conjunction with WHERE clause :
        
        ```sql
        UPDATE table_name SET column_name = new_value WHERE id = id_value;
        ```
        
- How to delete an entry from a table ?
    - You can use the DELETE command as follows :
        
        ```sql
        DELETE FROM table_name WHERE id = id_value;
        ```
        
- SQL Filter Words.
    - Where
        - Filter using some condition.
        - You can for example delete entries that their name is “jojo” using `DELETE FROM my_table WHERE name = ‘jojo’;`
        - You can of course delete a single row using the id.
    - Limit
        - Limits the number of responses from query.
        - So for example, we want to get only 5 rows from our table, we’d use → `SELECT * FROM table_name LIMIT 5;`
        - It’s not yet a useful filter word because the rows are not orders, so it’d be used with an ordering word.
    - Between
        - Selects data between two values.
        - So for example, we want to know the purchases happen between two dates →
            
            ```sql
            SELECT purchase_name FROM cart WHERE purchase_date BETWEEN '2022-7-30' AND '2022-8-30';
            ```
            
    - Like
        - Identifies content that matches based on patterns.
        - So for example, I want to search for all animals such that their names contain “lion” string, so it should return values like “lion” or “sea lion” for example.
            
            ```sql
            SELECT name, description FROM animals WHERE name LIKE '%lion%';
            ```
            
        - Notice that the percentage sign is a wild card character, which means that the string ‘lion’ might be a part of a bigger name, and this segment of a string lies between 0 or more characters. So `%lion%` might be “sea lion” or “lion” or “lion 2”.
        - In case you’re sure that a string starts or ends with a specific set of characters, you can modify the place of the wild card character. In other worlds, `%lion` would return “sea lion” whereas `lion%` would return something like “lion fish”.
    - IS NULL or IS NOT NULL
        - This is useful to check for null values in your tables.
        - So for example, you can get the rows which their animal name is null :
            
            ```sql
            SELECT description, id FROM animals WHERE name IS NULL;
            ```
            
- Common SQL Mistakes
    - Double Quotes instead of Single Quotes.
        - In PostgreSQL, double quotes always denotes delimited identifier. An identifier is the name of an object within PostgreSQL, which might be a table name or a column name.
        - Notice that, identifiers with double quotes are case sensitive. So “customer” is not the same as “Customer” or “CUSTOMER”.
        - Unquoted identifiers are case insensitive, so Customer is same as customer.
        - So use double quotes sparingly for better compatibility.
        - A single quote is used to specify that a token is a string. So you can assign a column value to be a string or use the WHERE clause to search for rows using a string.
    - Missing Semicolon
        - It’s really easy to for get to add a semicolon to a SQL statement. So it’s recommended to keep an eye on the beginning of a terminal line, so make sure it ends with this `=#` and not something like `-#`. Note that the latter waits for you to finish the statement (which is done by inserting a semicolon).
- How to create an Enum or a custom type ?
    - Some columns should accept certain values. So to describe a shop’s status, you might think of “open” and “closed” status and nothing else. Using an enum for this case would help in avoiding any other values except these two.
    - You can do so using →
        
        ```sql
        CREATE TYPE type_name AS ENUM ('value1', 'value2');
        ```
        
- What does `RETURNING` clause do ?
    - `RETURNING` clause avoids extra SQL statements, so it mainly helps in retrieving values of columns that were modified by an insert, update or delete.
    - Without `RETURNING`, you’d need to run a `select` query after you change some values in the rows.
        
        ```sql
        INSERT INTO articles (title, content) VALUES('test', 'test') RETURNING *
        ```
        
    - For more info, check [here](https://dzone.com/articles/use-returning-clause-to-avoid-unnecessary-sql-stat).
- CRUD and Filter Cheat Sheet.
    - ****Tips and Tricks****
    • You know that you're in the right database when you see the name of the database at the beginning of the terminal line.
    • If you already know the name of the database you want to connect to, you can write `psql name_of_database` and that would be equivalent to `psql postgres` `\c name_of_database`
    • Remember to steer clear of double quotes around strings in your queries!
    ****
    - **SQL Cheat Sheet**
        
        **Meta Commands**
        
        • `\l` **List** databases
        • `\c` **Connect** to a database
        • `\dt` **Display Tables** in a database
        • `\q` **Quit** out of psql to normal terminal
        
        **Queries**
        
        • CREATE `INSERT INTO worlds (name) VALUES ('Asgard');`
        • READ `SELECT* FROM herbs;`
        • UPDATE `UPDATE herbs SET sighting_date = '2021-01-10' WHERE id='1';`
        • DELETE `DELETE FROM herbs WHERE id='1';`
        • **Filters**
            ◦ BETWEEN`SELECT * FROM trips WHERE start_date BETWEEN '2021-02-01' AND '2021-02-12';`
            ◦ LIKE `SELECT * FROM books WHERE title LIKE '%ship%';`
        
- What are Foreign Keys, why they’re useful and how to use them ?
    - So far, we haven’t discussed how to relate one table to another.
    - This can be done via a foreign key that is stored in one row of a table which references a primary key in another row of another table.
    - For example, say you have a plants table and a region table. Each plant may have a region_id so you can get the plants that exist in a specific region or to know what plants does a region have.
    - This would become handy later in relations.
    - So while creating a child table, you can add a column that references another column in another table as follows :
        
        ```sql
        CREATE TABLE animals ( id SERIAL PRIMARY KEY, region_id REFERENCES regions(id)...);
        ```
        
- How to count the number of results we get from a query?
    - You can use the COUNT aggregate function like this :
        
        ```sql
        SELECT COUNT(*) FROM my_table WHERE addition_date BETWEEN '2022-8-1' AND '2022-9-1';
        ```
        
    - This would return the number of entries returned which their addition date (a column name that we added) is between these two dates.
- What are aggregate functions in SQL ? Define some types of aggregate functions.
    - An aggregate function in SQL performs a calculation on multiple values and returns a single value. SQL provides many aggregate functions that include avg, count, sum, min, max, etc. An aggregate function ignores NULL values when it performs the calculation, except for the count function.
    - Check [here](https://www.simplilearn.com/tutorials/sql-tutorial/sql-aggregate-functions#:~:text=An%20aggregate%20function%20in%20SQL%20performs%20a%20calculation%20on%20multiple,except%20for%20the%20count%20function.) to know the various types of aggregate functions.
    

## Lesson 3 : Create an API with a PostgreSQL connection.

- Lesson outcomes.
    - By the end of this lesson, you should know :
        - How to connect Node app with a database.
        - The role of environment variables.
        - Database migrations.
        - Testing models.
- Where do databases run ?
    - You can run a database on you computer and connect to it **locally** kind of like localhost.
    - You can run database on your own computer but in a **container system** like Docker.
    - Container systems might also be remotely, so you’re connecting to a database that is running in a **virtual machine**.
    - There’re also services like AWS or Azure provide databases in **the cloud**.
    - Notice that, **the more layers or technologies** between you and the database, the **more complex** it will be to connect to that database.
- What are environment variables and how to use them ?
    - Environment variables are used to store keys and passwords to connect with databases or APIs. You can also define different variables for different environment. For example, production might have different postgres user and hence different password than a development environment.
    - We create an env file to store different configurations for different environment. It’s important to note that the env file contains important information that cannot be shared in a public repo, so it should be added to `gitignore`file.
    - You can use `dotenv`package so you can modify the `env`object inside the `process` object by just calling `dotenv.config()`.
    - Notice that `dotenv.config()` method should be called as early as possible, so you would be able to use the correct environment variables.
    - It’s preferable to use destructuring syntax so you can extract the properties you need from the `process.env` object.
- How to connect to a PostgreSQL database ?
    - You need to have an `.env` file that has some configuration to connect to a database.
        
        ```
        POSTGRES_HOST = 127.0.0.1
        POSTGRES_DB = fantasy_worlds
        POSTGRES_USER = magical_user
        POSTGRES_PASSWORD = password123
        ```
        
    - You can use the pg package that facilitates the connection step between NodeJS and PostgreSQL.
        
        ```tsx
        import dotenv from "dotenv";
        
        import { Pool } from "pg";
        
        dotenv.config();
        
        const { POSTGRES_HOST, POSTGRES_DB, POSTGRES_USER, POSTGRES_PASSWORD } =
          process.env;
        
        const client = new Pool({
          host: POSTGRES_HOST,
          database: POSTGRES_DB,
          user: POSTGRES_USER,
          password: POSTGRES_PASSWORD,
        });
        
        export default client;
        ```
        
    - Pool is an object that represents one or more connections to a database.
- What are migrations ? and how they’re useful ?
    - Consider a case in which you and a co-worker are working on the same project but with different tasks.
    - Each one of you has created new tables to the database. Now when one of you pulls the other’s work, there’s an issue that your co-worker’s tables don’t exist in your environment.
    - A tedious way is to ask your co-worker for the commands he/she uses to create the tables.
    - A better idea would be if there’s a way to record the changes that made to the **schema** of the database and with a documented instructions to how to implement and rollback these changes.
    - So migrations are the record we’d use for such task.
    - Migration are useful in keeping our databases in sync across various environments.
    - To find more info about migrations, click [here](https://www.prisma.io/dataguide/types/relational/what-are-database-migrations).
- How to create migrations in Node ? What is the difference between up migration and down migration ?
    - Install the global package `npm install -g db-migrate db-migrate-pg`
    - Add a `database.json` reference file in the root of the project. Later, when we are working with multiple databases - this will allow us to specify what database we want to run migrations on. Here is an example **`database.json`**, you will just need to change the database names:
    - Notice that parameters like “user” or “database” changes depending on the name of PostgreSQL user and the databases that is being used.
        
        ```json
        {
          "dev": {
            "driver": "pg",
            "host": "127.0.0.1",
            "database": "fantasy_worlds",
            "user": "magical_user",
            "password": "password123"
          },
          "test": {
            "driver": "pg",
            "host": "127.0.0.1",
            "database": "fantasy_worlds_test",
            "user": "test_user",
            "password": "password123"
          }
        }
        ```
        
    - Create a migration by typing down `db-migrate create <table_name-table> --sql-file` to the terminal.
    - This creates a **migrations** folder, which has two sql files (up and down files) for each table and a JS file.
    - You can write SQL commands in these files.
    - Up files are used to create tables, update columns or any other change in the schema.
        
        ```sql
        CREATE TABLE mythical_weapons (
          name VARCHAR(100),
          type VARCHAR(50),
          weight integer,
          id SERIAL PRIMARY KEY
        );
        ```
        
    - Down files hold SQL commands that undo any changes that was made by the up files.
        
        ```sql
        DROP TABLE mythical_weapons;
        ```
        
    - So Up & Down Migrations are migrations that just run the commands in either file. So in Up Migration, you create changes. Whereas in Down Migration, you remove these changes.
        
        ![Untitled](Creating%20an%20API%20with%20PostgreSQL%20and%20Express%201eaa9c7e3d664358a31feb7064170400/Untitled.png)
        
    - Bring the migration up `db-migrate up`
    - Bring the migration down `db-migrate down`
    - There’s an important thing to note, the list of migration we executed is stored in a table called `migrations`. This table stores a list of migrations that are needed to be executed.
    - So if you want to remove the migration folders from the project, you also need to drop the `migrations` table.
- What are models ? and how execute SQL queries in Node ?
    - Models are the representation of the tables in a database in our code.
    - Each model performs various queries on its associated table.
    - A table name is plural because it holds many data (rows) of same type.
    - However, the model name is singular because it defines what would a row structure look like (properties/columns).
    - So each row would be an instance of the model class.
    - So let’s create a model that execute queries on our `mythical_weapon` table we created before.
        
        ```tsx
        // mythical_weapon.ts file 
        
        import Client from "../databases";
        
        export type Weapon = {
          id: number;
          name: string;
          type: string;
          weight: number;
        };
        
        export class MythicalWeaponStore {
          /// Fetches all items in the table.
          async index(): Promise<Weapon[]> {
            try {
              const conn = await Client.connect();
              const sql = "SELECT * FROM mythical_weapons";
              const result = await conn.query(sql);
              conn.release();
              return result.rows;
            } catch (e) {
              throw new Error(`Cannot get weapons ${e}`);
            }
          }
        }
        ```
        
    - So we utilized the client we created using the `Pool` class.
    - We need to define a type for our rows in the table since all rows share the same properties (columns).
    - We then establish a connection to the database using `Client.connect()` method which might throw an exception thus wrapped in a try/catch block.
    - After we’re done with the queries, we should release the connection.
    - Note that we add **Store** postfix which means table in our code.
- Full CRUD methods for `MythicalWeaponStore` model.
    
    ```tsx
    import Client from "../databases";
    
    export type Weapon = {
      id: number;
      name: string;
      type: string;
      weight: number;
    };
    
    export class MythicalWeaponStore {
      /// Fetches all items in the table.
      async index(): Promise<Weapon[]> {
        try {
          const conn = await Client.connect();
          const sql = "SELECT * FROM mythical_weapons";
          const result = await conn.query(sql, []);
          conn.release();
          return result.rows;
        } catch (e) {
          throw new Error(`Cannot get weapons ${e}`);
        }
      }
    
      async show(id: number): Promise<Weapon> {
        try {
          const conn = await Client.connect();
          const sql = "SELECT * FROM mythical_weapons WHERE id=($1)";
          const result = await conn.query(sql, [id]);
          conn.release();
          return result.rows[0];
        } catch (e) {
          throw new Error(`Cannot get weapons ${e}`);
        }
      }
      async create(weapon: Weapon): Promise<Weapon> {
        try {
          const conn = await Client.connect();
          const sql =
            "INSERT INTO mythical_weapons (id, name, type, weight) VALUES ($1, $2, $3, $4) RETURNING";
          const result = await conn.query(sql, [
            weapon.id,
            weapon.name,
            weapon.type,
            weapon.weight,
          ]);
          conn.release();
          return result.rows[0];
        } catch (e) {
          throw new Error(`Cannot get weapons ${e}`);
        }
      }
    
      async delete(id: string): Promise<Weapon> {
        try {
          const conn = await Client.connect();
          const sql = "DELETE FROM mythical_weapons WHERE id=($1)";
          const result = await conn.query(sql, [id]);
          conn.release();
          return result.rows[0];
        } catch (e) {
          throw new Error(`Cannot get weapons ${e}`);
        }
      }
    }
    ```
    
- What is the difference between Unit and Integration testing. Why we might consider testing models as an integration test?
    - A **unit test**, tests a small chunk of code in your application. Unit tests are for the individual functions or classes in your code, to make sure each one is doing what you need. These are small, typically fast to write, and can really save you time when trying to understand where a problem is happening in the program.
    - An **integration test** checks how the individual pieces of your application logic work together. The span of one integration test will cover multiple chunks of code (that can and should each have their own unit tests) and make sure that working correctly together in a flow or process.
    - Models testing can be considered as integration tests because they test a flow in the application from model to database and back. Its not a large process, so they won't look very different from unit tests, but it is a good opportunity to talk about the differences.
- How to test a model?
    - So if you want to test a model, you can’t just run CRUD methods on your production database, you need a separate one.
    - This means that we’d create a test database that is the same as our production database in terms of schema but it might be empty or has data that we know about so our tests can be predictable.
    - Let’s head to `database.json` and add a testing environment →
        
        ```json
        {
          "dev": {
            "driver": "pg",
            "host": "127.0.0.1",
            "database": "fantasy_worlds_dev",
            "user": "postgres",
            "password": "01004895720"
          },
          "test": {
            "driver": "pg",
            "host": "127.0.0.1",
            "database": "fantasy_worlds_test",
            "user": "postgres",
            "password": "01004895720"
          }
        }
        ```
        
    - You add any type of database (MySQL, PostgreSQL, MongoDB, etc.) to this file, and you can also add multiple environments for the same test file.
    - Recall that we used `dotenv` package to create `.env` file and use that file to store API keys or passwords. So we store these credentials to switch between environments while running test scripts for example.
    - So you need to have more environment variables depending on how many environments you have →
        
        ```tsx
        POSTGRES_HOST = 127.0.0.1
        POSTGRES_DB = fantasy_worlds_dev
        POSTGRES_DB_TEST = fantasy_worlds_test
        POSTGRES_USER = postgres
        POSTGRES_PASSWORD = 01004895720
        ENV=test
        ```
        
    - Let’s modify `databases.ts` file so that we can make conditional connection to a database depending on the environment.
        
        ```tsx
        import * as dotenv from "dotenv";
        import { Pool } from "pg";
        
        dotenv.config();
        const {
          POSTGRES_HOST,
          POSTGRES_DB,
          POSTGRES_USER,
          POSTGRES_PASSWORD,
          ENV,
          POSTGRES_DB_TEST,
        } = process.env;
        
        let client: Pool;
        if (ENV === "test") {
          client = new Pool({
            host: POSTGRES_HOST,
            database: POSTGRES_DB_TEST,
            user: POSTGRES_USER,
            password: POSTGRES_PASSWORD,
          });
        }
        if (ENV === "dev") {
          client = new Pool({
            host: POSTGRES_HOST,
            database: POSTGRES_DB,
            user: POSTGRES_USER,
            password: POSTGRES_PASSWORD,
          });
        }
        // @ts-ignore: ts(2454)
        export default client;
        ```
        
    - You can load your stores, and test the result of each method of your models using jasmine.
    - After you create Spec file for your model and start writing unit tests, you need to add the following script to your `Package.json`file.
        
        ```tsx
        "test": "SET ENV=test&& db-migrate --env test reset && db-migrate --env test up && npx tsc && npx jasmine && db-migrate --env test reset"
        ```
        
        Notice that you might need to use `cross-env`  package if set command doesn’t work with you (especially in Windows).
        
    - Let’s slice the previous script we wrote.
        - `set ENV=test` this changes the ENV variable in the `.env` file to “test” rather than “dev”. **Don’t put spaces after the value.**
        - `db-migrate --env test reset` runs all down migrations so in case the previous test run fails, this would remove the previously created tables.
        - `db-migrate —env test up` runs the up migration on `test` database. Test database is the database you defined in `database.json` file. Note that `-env` flag specifies the environment.
        - `npx tsc` used to transpile TS to JS.
        - `jasmine` runs the test specs for transplied JS files.
        - `db-migrate --env test reset` runs down migration on `test` database in case all tests pass so that next test run wouldn’t use the previous tables.
        
    - The `$1` represents a parameter in the query, so the first item in the array parameters is filled in the query and so on. Therefore `id` variable in the parameters array are passed to `$1`.
    - Learn more about `db-migrate` commands from [here](https://db-migrate.readthedocs.io/en/latest/Getting%20Started/commands/).

## Lesson 4 : Create an API with Express.

- Lesson outcomes.
    - This lesson is all about the client-facing side of our API. We'll cover the following topics
        - RESTful API structure
        - Express for incoming requests
        - Breaking Express routes into separate files
        - Mapping RESTful routes to model methods
        - Testing routes
    - In this lesson, it’d be useful to know about MVC design pattern. Click [here](https://www.freecodecamp.org/news/understanding-the-basics-of-ruby-on-rails-http-mvc-and-routes-359b8d809c7a/) to know about MVC concept, the article discusses the concept with RoR but the same concept stands.
- What does RESTful API mean ? Also what are RESTful routes for an API ?
    - RESTful → **Re**presentational **S**tate **T**ransfer(-ful) Application Programming Interface.
    - REST is an architectural pattern to organize an API endpoints.
    - Recall that HTTP verbs are like GET, POST, PATCH, UPDATE, DELETE, etc..
    - Continuing on the `mythical_weapons` table we created, let’s discuss various routes of REST pattern
        - INDEX
            - `/mythical-weapons → Get` is called an **index** route which returns all the properties as a list for all items of this type in the database
        - SHOW
            - **`/mythical-weapons/:id → Get`** is similar to the index route except that it takes an id parameter that is used to return a single item.
        - CREATE
            - `/mythical-weapons -> Post` this has the same URL as the index route but with different HTTP verb. This create a new item to the related database and returns a copy of that new item.
            - The object is passed in the request body.
        - EDIT
            - `/mythical-weapons/:id -> PUT/PATCH` this is the update route which specifies the id of the item’s properties we want to update.
            - This returns a copy of the updated item.
            - The properties we want to update is passed via the request’s body.
        - DELETE
            - `/mythical-weapons/:id -> DELETE` this is delete route in which we specify the id of the item we want to delete.
            - It usually returns the deleted item.
    - Example request on express.
        
        ```tsx
        const app = express();
        
        const address = "0.0.0.0:3000";
        
        app.use(body.Parser.json());
        
        app.get("/weapon", function(req,res) {
        	const weapons = {}; // We should call mode.index here for the index route.
        	return res.json(weapons);
        } );
        ```
        
        - This is an index route which fetches all the weapons available.
        - Recall our Model which was :
            
            ```tsx
            import Client from "../databases";
            
            export type Weapon = {
              id: number;
              name: string;
              type: string;
              weight: number;
            };
            
            export class MythicalWeaponStore {
              /// Fetches all items in the table.
              async index(): Promise<Weapon[]> {
                try {
                  const conn = await Client.connect();
                  const sql = "SELECT * FROM mythical_weapons";
                  const result = await conn.query(sql, []);
                  conn.release();
                  return result.rows;
                } catch (e) {
                  throw new Error(`Cannot get weapons ${e}`);
                }
              }
            
            /// .....
            }
            ```
            
        - This is why we called the model methods these names, so it can be the same as the RESTful routes.
        
- What is CORS ?
    - CORS stands for **Cross Origin Resource Sharing**.
    - Typically, a browser can make requests if the API have the same domain from which the request has been made. If they don’t share the same domain, the client-side domain must be whitelisted by CORS in the API in order to have access.
    - In other words, if you want to make your API accessible publicly then you have to add CORS to your API.
    - What if my front-end and backend have the same domain ? Or my API is only consumed by my front-end ? CORS is not needed since the URLs are the same.
    - CORS is supported by all browser, so it’s your choice whether you want your API to be accessible by other domains or not.
- How to use CORS in Express ?
    - First things first, you need to check the docs from [here](https://expressjs.com/en/resources/middleware/cors.html).
    - We should install cors library and its type definitions.
        
        ```powershell
        npm install cors
        ```
        
    - Here’s a simple setup that you can initially follow →
    - We can start by allows CORS for all domains :
        
        ```tsx
        import express from 'express';
        import cors from 'cors';
        
        var app = express()
        
        app.use(cors())
        
        app.get('/products/:id', function (req, res, next) {
          res.json({msg: 'This is CORS-enabled for all origins!'})
        })
        
        app.listen(80, function () {
          console.log('CORS-enabled web server listening on port 80')
        })
        ```
        
    - We can configure CORS on app level (all routes) like we did above or route level (specific routes).
    - So on a single route, you can do the following :
        
        ```tsx
        import express from 'express';
        import cors from 'cors';
        var app = express()
        
        app.get('/products/:id', cors(), function (req, res, next) {
          res.json({msg: 'This is CORS-enabled for a Single Route'})
        })
        
        app.listen(80, function () {
          console.log('CORS-enabled web server listening on port 80')
        })
        ```
        
    - But what if I want to whitelist only a specific domains ? Let’s see →
        
        ```tsx
        import express from 'express';
        import cors from 'cors';
        var app = express()
        
        var corsOptions = {
          origin: 'http://example.com',
          optionsSuccessStatus: 200 // some legacy browsers (IE11, various SmartTVs) choke on 204
        }
        
        app.get('/products/:id', cors(corsOptions), function (req, res, next) {
          res.json({msg: 'This is CORS-enabled for only example.com.'})
        })
        
        app.listen(80, function () {
          console.log('CORS-enabled web server listening on port 80')
        })
        ```
        
    - You might notice CORS is just a middleware that we add to a specific request method.
- What should I do if the third-party API I’m using doesn’t support CORS and I can’t use it in my front-end ?
    - The plea above is a common one developers struggle with.
    - First, how do you know the API doesn't support CORS? If you are making a normal fetch request to an endpoint the API says it supplies, but are getting an HTTP error similar to this one:
    
    ```
    Reason: Did not find methodin CORS header ‘Access-Control-Allow-Methods’
    
    ```
    
    - Then you might be working with an API that doesn't support CORS. To make certain, you can read more into the documentation of the API, or, another quick trick is to open [Postman](https://www.postman.com/) or another endpoint testing tool and try the exact same request there. Postman is not a browser and does not require CORS support, so if your request works from Postman but not from the browser, it is pretty much confirmed that your issue is that the API doesn't support CORS. This is a major failure on the API's side, CORS support is pretty much required in order to be useful to modern web applications, but you still see this problem around on older APIs from time to time.
    - When selecting APIs for your project, you should definitely look for which ones are CORS enabled. But, if you really must use one that isn't -- don't panic -- it is still possible. The issue is that CORS support is required **by browsers**. So the solution is to not make the request from the front end. Your back end will have to make the request to the API. So you can make a custom endpoint in your API that **IS** accessible from your front end, and that API endpoint will trigger a request to the actual API you want to use. Once it gets a response from that API, your back end will just pass that information to the frontend. It is more complicated than it should be, but its a 'best of a bad situation' solution. That is why in this course we only teach you to make APIs with CORS support!
- How to expose the API of the models (stores) to the server app?
    - First thing you need to do is to create a `handlers` folder inside `src` folder in which you create a **handler** for each **model**.
    - Each handler is responsible of creating RESTful routes (index, show, delete, update, etc.) that are equivalent with the model’s methods.
    - So our `mythical_weapon_handler.ts` should look like this :
        
        ```tsx
        import express, { Request, Response } from "express";
        import { MythicalWeaponStore, Weapon } from "../models/mythical_weapon";
        
        const store = new MythicalWeaponStore();
        
        const index = async (_req: Request, res: Response) => {
          const weapons = await store.index();
          res.json(weapons);
        };
        
        const mythical_weapon_routes = (app: express.Application) => {
          app.get("/product", index);
        };
        
        //.... Should have all methods for other RESTful routes.
        
        export default mythical_weapon_routes;
        ```
        
    - Now why would we accept the express app object to the `mythical_weapon_routes` ?
    - Think of exporting all of the RESTful routes of `mythical_weapon` to the express app, that would be a lot of middlewares to import and to fill our `server.ts` file with.
    - Instead, we can just use `mythical_weapon_routes` function that would utilize the app inside.
    - So `server.ts` would look like this :
        
        ```tsx
        import express, { Request, Response } from "express";
        import mythical_weapon_routes from "./handlers/mythical_weapons";
        
        const app = express();
        const port = 3000;
        
        app.get("/", (req, res) => {
          res.send("Hola amigo");
        });
        
        mythical_weapon_routes(app);
        
        app.listen(port, () => console.log("app starts on : http://localhost:3000"));
        ```
        
    - So we have less methods to import with this way.
- How things really work in the big picture ?
    1. The client (a browser or any service that uses that API) makes a request to our server.
    2. The express app navigates to the correct route given by the client and hence go to the correct handler.
    3. The handler then accesses the correct store (model) and call a method in that model (index, show, delete, etc.).
    4. The model accesses the database and then returns the correct data (list of items, etc.).
    5. The data is given back to the handler and a response is then sent with the requested data.

## Lesson 5 : Authentication and Authorization in a Node API.

- Lesson outcomes.
    - This lesson is all about security. We need to protect information in our database and handle things like user authentication. So the following topics are covered :
        - Password hashing and salt.
        - Implementing the **bcrypt** library for password hashing.
        - Introduction to JWT’s and how they’re important for authentication and authorization.
        - Implementing JWT’s with the library **json-web-token**.
    - To know more about JWT and its available libraries, check [here](https://jwt.io/).
- Why does data security considered to be important ?
    - When we store general information like products, items or vendor details, these information are insensitive.
    - However, a user table might have information that needs to be protected like passwords, IDs, even emails or credit card information.
    - Any attacker might maliciously use these data if they got a hold of it.
- How to protect passwords ?
    - First thing, you should never store plain text passwords in your database nor in your code.
    - Password **Hashing** and **Salt** obscure passwords, so raw password strings are never stored or persisted in the database.
- What is hashing ? what is the main drawback of weak hashing functions ?
    - Hashing is to run the password through a function which would generate a seemingly random letters and numbers.
    - Minor changes in the input will result in completely different outputs.
    - Same input will get the same output for password checking.
    - Hashing is a one way operation. In other words, the hashed password cannot be reversed to get the original password.
    - The main drawback is the reverse lookups where a hash is compared against a dictionary of hashes and their associated passwords.
- What is salt and pepper ?
    - Salt is the process of adding a random string to every password.
    - This helps in avoiding brute-force attacks due to this random string appended at the beginning or at the end.
    - The salt or the random string should be secret and stored in an environment variable or in the database.
    - Pepper might be the string added to the original password and the salt might be just an integer.
    - It’s recommended to use pepper in the content, however, you shouldn’t really use it and [here](https://stackoverflow.com/questions/16891729/best-practices-salting-peppering-passwords) is why.
- What is `bcrypt` and how to use it ?
    - `Bcrypt` is a very common library for implementing password encryption.
    - To use it, install it via `npm` →
        
        ```bash
        npm i bcrypt
        npm i --save-dev @types/bcrypt
        ```
        
    - You need to go to the `.env` file to add the necessary environment variables :
        
        ```
        BCRYPT_PASSWORD=your-secret-password
        SALT_ROUNDS=10
        ```
        
    - You can use the function as follows →
        
        ```tsx
        const hash = bcrypt.hashSync(user.password + pepper + parseInt(saltRounds);
        ```
        
    - Kindly note that pepper variable is basically BCRYPT_PASSWORD variable we added to `.env` file. After that, we can save the hash as the password of the user in the database.
    - Now to check if the password of a signed in user is valid, we would use `bcrypt.compareSync()` method as follows →
        
        ```tsx
        bcrypt.compareSync(password+pepper, user.password_digest)
        ```
        
    - Be aware that maybe the user enters a username that doesn’t exist, so be careful with handling such case.
        
        ```tsx
        /// Method that exist in Users model.
        async authenticate(username: string, password : string) : Promise<User | null) {
        
        	const conn = await Client.connect();
        	const sql = 'SELECT password_digest FROM users WHERE username=($1)';
        	const result= await conn.query(sql, [username]);
        
        	// To handle if the username not found
        	if(result.rows.length){
        		const user = result.rows[0];
        		console.log(user);
        		if(bcrypt.compareSync(password, user.password_digest)){
        			// Correct user found, return it
        			return user;
        		}
        	}
        	
        	return null
        }
        ```
        
- What are JWTs ? what is the problem with sessions concept? How does JWT offer a better solution for authentication?
    - JWT stands for JSON Web Token. It’s the most common mean for authenticating users in decoupled (separate front-end and backend) web apps.
    - They’re secure digital token that can be passed between your front-end and back-end applications to authenticate users and even store important user information.
    - Initially, when a user makes an authentication request and it’s successful, a session ID is sent back for the user so he can use it for subsequent requests.
    - The API server has to store a table called “sessions” that has a pair of session ID and it’s associated user ID.
    - The problems of that approach are :
        - It takes time to validate the session ID (it takes time to lookup for the associated user id).
        - Harder to maintain and manage. So if you’re using a microservice architecture, that would be hard to maintain because any change in sessions table must propagate to other services.
    - To address these problems, we need something that is stateless. Stateless means that the server knows that the token is valid and works.
    - So in a microservice architecture where the authentication service is separated from API server, the API server must fetch the public key once the user is authenticated so the API server can valid that token for any subsequent requests.
        
        ![Untitled](Creating%20an%20API%20with%20PostgreSQL%20and%20Express%201eaa9c7e3d664358a31feb7064170400/Untitled%201.png)
        
    
- What are the parts of JWTs? Discuss each part separately.
    - A JWT is just a long string.
        
        ![Untitled](Creating%20an%20API%20with%20PostgreSQL%20and%20Express%201eaa9c7e3d664358a31feb7064170400/Untitled%202.png)
        
    - This string consists of three parts :
        - **Header**.
        - **Payload**.
        - **Signature**.
            
            ![Untitled](Creating%20an%20API%20with%20PostgreSQL%20and%20Express%201eaa9c7e3d664358a31feb7064170400/Untitled%203.png)
            
    - These parts work together to ensure the information within JWT is **consistent** and we can **validate** that the information within the token has not been changed.
    - The header and the payload data are encoded using a Base64 algorithm. After that, the signature is generated by adding both the header and the payload and encoding the addition using HS256 algorithm.
    - It’s important to note that Base64 encoding scheme can be encoded/decoded so given the right string, we can get the correct header. It’s not the case with the signature as it’s only a one way process.
        
        ![Untitled](Creating%20an%20API%20with%20PostgreSQL%20and%20Express%201eaa9c7e3d664358a31feb7064170400/Untitled%204.png)
        
    - Let’s discuss each part in more detail :
        - Payload
            - After decoding the JWT received, we can use the user object that has the following data :
                
                ```json
                {
                	"user" : "gabe",
                	"school" : "udacity",
                	"role" : "instructor"
                }
                ```
                
            - We said that Base64 can be decoded easily for anyone that has the JWT, so you should **never** store important data like passwords/phone number/social number in the payload.
            - The payload mainly helps in identify the user who is making the requests, so we’d make use of the username or typically the user ID to fulfill the requests.
        - Header
            - The header includes the algorithm used for decoding and encoding which might be HS256 (HMAC using SHA256). This algorithm used to mix encode the addition of the header and the payload.
            - **HS256** and **RS256** are commonly used encryption algorithms. Check the difference from [here](https://stackoverflow.com/questions/39239051/rs256-vs-hs256-whats-the-difference).
                
                ```json
                {
                	"alg" : "HS256",
                	"type" : "JWT"
                }
                ```
                
        - Signature
            - Signature is the last part in our JWT. It makes sure that the received token authentic and has not been tampered with.
            - Recall the key we received from the authentication service, we still haven’t used it right? We use it in the function that generates the HS256 string.
                
                ![Untitled](Creating%20an%20API%20with%20PostgreSQL%20and%20Express%201eaa9c7e3d664358a31feb7064170400/Untitled%205.png)
                
            - So if a third-party doesn’t have the secret, they can’t sign the information within their payload or header.
            - Note that any change in the header/payload would result in a different signature.
                
                ![Untitled](Creating%20an%20API%20with%20PostgreSQL%20and%20Express%201eaa9c7e3d664358a31feb7064170400/Untitled%206.png)
                
            - So we encode both the header and payload and concatenate them. We pass the encoded header and payload as well as the secret to the HS256 (HMACSHA256).
            - So to validate a received JWT, we can extract the header and the payload and do the same process we just done and compare the JWT generated with the one received.
- What is the difference between Authentication and Authorization ?
    - In simple terms, authentication is the process of verifying who a user is, while authorization is the process of verifying what they have access to.
    - Comparing these processes to a real-world example, when you go through security in an airport, you show your ID to authenticate your identity. Then, when you arrive at the gate, you present your boarding pass to the flight attendant, so they can authorize you to board your flight and allow access to the plane.
- Describe the authentication flow.
    - The user first signs in/up and the API server returns a token to the client.
    - The client stores that token for any subsequent requests to the server.
        
        ![Untitled](Creating%20an%20API%20with%20PostgreSQL%20and%20Express%201eaa9c7e3d664358a31feb7064170400/Untitled%207.png)
        
- How to create a JWT ?
    - You have to install `jsonwebtoken` package via `npm i jsonwebtoken`
    - You can creating a token as follows →
        
        ```tsx
        import jwt from 'jsonwebtoken';
        
        const create = async (req, res) => {
        
        	const user : User = {
        		username : req.body.username,
        		password : req.body.password
        		}
        	// Passwords needs to be hashed before creating a new user, but for the sake of simplicity
        	// we ignored it here.
        	const newUser = await store.create(user);
        	const token = jwt.sign({user : newUser}, process.env.TOKEN_SECRET);
        	res.json(token);
        }
        ```
        
    - So given the username and the password, we returned the token. A question might arise, why not returning the user ?
    - Recall that the client can decode the JWT and extract the user info from the payload part of the JWT.
- Why should the client send the token inside the header not the body ?
    - It’s a part of HTTP standard so JWT tokens should be sent as a Bearer tokens in the authorization header.
    - This adds more security.
    - Notice that there’re many types of authorization headers that people can use and you can verify the token depending on its type.
        
        ```markdown
        			 •    Basic Auth
               •    Bearer Token
               •    API Key
               •    Digest Auth
               •    Oauth 2.0
               •    Hawk Authentication
               •    AWS Signature
        ```
        
    - So we should send it inside the `Authorization` key in the header using the following format :
        
        ```tsx
        Authorization: Bearer <token>
        ```
        
- Why validating a JWT is important ? How to verify if a JWT is valid ?
    - Validating a JWT is crucial because we don’t want, for example, a user to edit other user’s credentials or have access to different users.
    - To extract the JWT, we have to check the `Authorization` key in the request header.
    - Recall from the previous question, the authorization header format is as follows :
        
        ```markdown
        Authorization: Bearer <token>
        ```
        
    - So you first need to access the authorization header and then split the string to extract the token :
        
        ```tsx
        const authorizationHeader = req.headers.authorization;
        const token = authorizationHeader.split(' ')[1];
        ```
        
    - We can then verify the JWT validity to make the requested operation.
        
        ```tsx
        const create = async (req: Request, res: Response) => {
            try {
                const authorizationHeader = req.headers.authorization
                const token = authorizationHeader.split(' ')[1]
                jwt.verify(token, process.env.TOKEN_SECRET)
            } catch(err) {
                res.status(401)
                res.json('Access denied, invalid token')
                return
            }
        
            //....rest of method is unchanged
        }
        ```
        
    - Notice that **401** status code means that the client request has not been completed because it lacks valid authentication credentials for the requested resource. In other words, **unauthorized request.**
    - Notice that `jwt.verify(...)` returns the decoded payload.
- What if we want to verify JWT for more than single route ?
    - So to avoid redundancy, we can create a middleware (which is basically a function) inside the handler file that is capable of verifying a token before proceeding with the request.
        
        ```tsx
        const verifyAuthToken = (req: Request, res: Response, next) => {
            try {
                const authorizationHeader = req.headers.authorization
                const token = authorizationHeader.split(' ')[1]
                const decoded = jwt.verify(token, process.env.TOKEN_SECRET)
        
                next();
            } catch (error) {
                res.status(401)
            }
        }
        ```
        
    - So if the JWT is valid, then proceed (calling `next()`) with the other request handler (which is a function that utilize a model’s method like index, show, etc.).
    - Finally, we can add this middleware to the routes:
        
        ```tsx
        const mount = (app: express.Application) => {
            app.get('/users', index)
            app.get('/users/:id', show)
            app.post('/users', verifyAuthToken, create)
            app.put('/users/:id', verifyAuthToken, update)
            app.delete('/users/:id', verifyAuthToken, destroy)
        }
        ```
        
    - So CREATE, UPDATE and DELETE routes require authorization check.
- How to decode JWT on the fly (maybe for testing a token that was received in Postman) ?
    - You can use the following website [jwt.io](https://jwt.io/) so you can decode.
    - So you can check if a token was tampered with by verifying if the secret word generates the same token received.
        
        ![Untitled](Creating%20an%20API%20with%20PostgreSQL%20and%20Express%201eaa9c7e3d664358a31feb7064170400/Untitled%208.png)
        
- Extra → [What is hashing and its uses ?](https://www.2brightsparks.com/resources/articles/introduction-to-hashing-and-its-uses.html)

## Lesson 6 : SQL for Advanced API Functionality.

- Lesson Outcomes.
    - Database relationships
    - SQL Joins
    - RESTful endpoints using with joins
    - RESTful endpoints with params.
    - Introduction to database relationships can be found [here](https://www.lifewire.com/database-relationships-1019729).
    - [A visual explanation of SQL Joins.](https://blog.codinghorror.com/a-visual-explanation-of-sql-joins/)
- Describe database relationships.
    - There’re three most common relationships in RDBMS :
        - One-to-Many
            - This is the most common relationship you’d find.
            - Recall the plants and regions example. Each plant can belong to a region, so  each plant row in the plants table has a foreign key (which was region id) of a region from regions table.
            - You can deduce that a set of plants can belong to the same region and a single region can contain a set of plants.
                
                ![Untitled](Creating%20an%20API%20with%20PostgreSQL%20and%20Express%201eaa9c7e3d664358a31feb7064170400/Untitled%209.png)
                
        - One-to-One
            - In this type, each row in a table can only references a single row in another table.
            - So for example, a single region can only contain a single type of plants and a single plant can only exist in a single region.
                
                ![Untitled](Creating%20an%20API%20with%20PostgreSQL%20and%20Express%201eaa9c7e3d664358a31feb7064170400/Untitled%2010.png)
                
        - Many-to-Many
            - Two tables has a relationship through an intermediary table.
                
                ![Untitled](Creating%20an%20API%20with%20PostgreSQL%20and%20Express%201eaa9c7e3d664358a31feb7064170400/Untitled%2011.png)
                
            - Consider a case where a car can be owned by multiple persons (a family) and also a person can own multiple cards. At first glance, it’s not obvious how to relate both tables, however, this can be achieved using a join table.
            - So consider an orders table (which references a user id but we don’t care about it for now) and a products table.
                
                ```sql
                CREATE TABLE orders (
                  id SERIAL PRIMARY KEY,
                  status VARCHAR(64),
                  user_id bigint REFERENCES users(id)
                );
                ```
                
                ```sql
                CREATE TABLE products (
                  id SERIAL PRIMARY KEY,
                  name VARCHAR(64) NOT NULL,
                  price integer NOT NULL
                );
                ```
                
            - The join table would reference both order id and product id as foreign keys.
                
                ```sql
                CREATE TABLE orders_products (
                  id SERIAL PRIMARY KEY,
                  quantity integer,
                  order_id bigint REFERENCES orders(id),
                  product_id bigint REFERENCES products(id)
                );
                ```
                
            - So a product can be in multiple orders, and an order can have multiple product.
                
                ![Untitled](Creating%20an%20API%20with%20PostgreSQL%20and%20Express%201eaa9c7e3d664358a31feb7064170400/Untitled%2012.png)
                
            - It’s important to note that join table won’t have its own model.
- How to add a foreign key in a row of a table that references another row in other table?
    - Consider an order than can be owned by a user (one-to-many relationship) :
        
        ```sql
        CREATE TABLE users (id SERIAL PRIMARY KEY, name text, age integer);
        ```
        
        ```sql
        CREATE TABLE orders (
          id SERIAL PRIMARY KEY,
          status VARCHAR(64),
          user_id bigint REFERENCES users(id)
        );
        ```
        
- How to insert data to join tables and where to put this logic ?
    - Insertion logic should be added to the primary entity. For orders and products example, orders are the primary entities that have products.
        
        ```tsx
        /// Inside orders.ts model.
        
        async addProduct(quantity:number, orderId: string, productId: string) : Promise<Order> {
        	try{
        		const conn = await Client.connect();
        		const sql = "INSERT INTO orders_products (quantity, order_id, product_id) VALUES($1, $2, $3)";
        		const result = await conn.query(sql,[quantity, orderId, productId]);
        		const order = result.rows[0]
        		conn.release();
        		return order;
        	}
        	catch(e){
        		throw new Error(`Could not add product ${productId} to order ${orderId}`);
        	}
        
        };
        ```
        
- How to create new route and handler function for creating entries inside join table ? (orders - products example).
    - A “post” HTTP verb should be used despite the fact that both the order and the product exist in their tables, however, we’re creating new entry (row) inside the join table.
    - Since we are adding products to a single order, we can define the following route →
        
        ```tsx
        const orderRoutes (app : Application) => {
        	app.get('/orders', index);
        	app.get('/orders/:id', show);
        	app.post('/orders', create);
        	/// We add a product to the products that is owned by
        	/// an order of :id.
        	app.post('/orders/:id/products', addProduct);
        
        }
        ```
        
    - So the `addProduct` method inside the handler file should look like this →
        
        ```tsx
        const addProduct = async (req, res) => {
        	
        	const orderId : string = req.params.id;
        	const productId : string = req.body.productId;
        	const quantity : number = parseInt(req.body.quantity);
        
        	try {
        		const addedProduct = await store.addProduct(quantity, orderId, productId);
        		res.json(addedProduct);
        	}
        	catch(e){
        		res.status(400);
        		res.json(e);
        	}
        
        }
        ```
        
- SQL commands for sorting.
    - There are a few more SQL commands that will really come in handy, all of these are for ordering the responses you get back from a query.
    - These commands allow you to order responses alphabetically or by a number. First, you choose the column that you want to use to order the rows, then you can choose the direction - ascending or descending. Here's an example:
        
        `SELECT * FROM products ORDER BY price DESC;`
        
    - This query would get you all rows and columns from the products table. We have chosen to use the price column as the piece of information we want to order by, and chosen DESC as the direction, so the response we see will be a list of all products where products with the highest prices would come first and get smaller as you scrolled down the list.
        
        `SELECT * FROM users ORDER BY name ASC;`
        
    - Same thing but with alphabetical order instead of numerical. This query would get all the rows and columns from the users table, and sort the rows by name starting with A and going up to Z.
- What are Joins in SQL ? Give an example and illustrate how to run a join query.
    - SQL Joins collate the columns of multiple tables that share a common column.
    - Recall the `products`, `orders` and `order_products` tables from the previous questions.
    - Consider a case where you want all products that exist only in orders. This can be easily envisioned as **Venn diagram**
        
        ![Untitled](Creating%20an%20API%20with%20PostgreSQL%20and%20Express%201eaa9c7e3d664358a31feb7064170400/Untitled%2013.png)
        
    - So we want the common products between two tables and this is called **inner join** which is the most common type of joins.
        
        ![Untitled](Creating%20an%20API%20with%20PostgreSQL%20and%20Express%201eaa9c7e3d664358a31feb7064170400/Untitled%2014.png)
        
    - The query should be like this
        
        ```sql
        SELECT * FROM products INNER JOIN order_products ON products.d = order_products.id;
        ```
        
    - This query means :
        - Fetch all columns (you may specify any column you want) from the inner join from `products` table and `order_products` table such that both product id in each table are equal.
    - It’s important to note that you can fetch the common row properties from both tables. For example, this query fetches name and price from products table whereas order_id, product_id and quantity comes from orders table.
        
        ```sql
        SELECT name, price, order_id, quantity, product_id FROM products INNER JOIN order_products ON product.id = order_products.id;
        ```
        
    - There’re different type of joins like full outer join, left outer join and many others. Check [here](https://blog.codinghorror.com/a-visual-explanation-of-sql-joins/) to know about other types.
- Where to put JOIN queries logic ? in which table ?
    - Usually, you shouldn’t really put the join query logic in either tables.
    - You should create a service file that is not specified for a single table and might orchestrates more than a single table.
- What are services ?
    - A **service file** is a place to write extra business logic that does not belong in a handler or a model or orchestrates changes with multiple models.
    - Note that the service should **only read information** from database, any other action should be done through models.
    - We need to define a **`services`** folder under **`src`**folder and add the service file to it.
    - As the complexity of our logic for authorizing which users can see various pages grows, the logic to check JWTs for authorization rights would become its own service.
- How can we create a service that joins orders and products table and return the result ?
    - We can create a service called `dashboard.ts` which would contain code like this :
        
        ```tsx
        import Client from '../database'
        
        export class DashboardQueries {
          // Get all products that have been included in orders
          async productsInOrders(): Promise<{name: string, price: number, order_id: string}[]> {
            try {
              //@ts-ignore
              const conn = await Client.connect()
              const sql = 'SELECT name, price, order_id FROM products INNER JOIN order_products ON product.id = order_products.id'
        
              const result = await conn.query(sql)
        
              conn.release()
        
              return result.rows
            } catch (err) {
              throw new Error(`unable get products and orders: ${err}`)
            } 
          }
        }
        ```
        
    - **Things to note from this:**
        - We import the database client and create a connection in the method just like a model, because this service is running queries on the database, they will just be READ-ONLY queries, instead of updating tables, so this is ok.
        - `productsInOrders` - sometimes, it is really hard to give a method a clear name, especially in situations like this. If you can't find a name that describes precisely what is going on, leave a comment like I did to explain what the name fails to convey.
        - Notice the return type from this typescript method -- it isn't a product, an order, or any other type we created in the models. This is another sign that we were right to put this method away in its own service rather than in products, it is returning a **hybrid** of two tables, and that would be messy to implement in any model file.
    - After that, we should create a separate handler file for these methods :
        
        ```tsx
        import express, { Request, Response } from 'express'
        
        import { DashboardQueries } from '../services/dashboard'
        
        const dashboardRoutes = (app: express.Application) => {
            app.get('/products_in_orders', productsInOrders)
        }
        
        const dashboard = new DashboardQueries()
        
        const productsInOrders = async (_req: Request, res: Response) => {
          const products = await dashboard.productsInOrders()
          res.json(products)
        }
        
        export default dashboardRoutes
        ```
        
    - **Things to note here:**
        - This looks mostly like any other handler we created, but we aren't importing a model type, instead we are importing `dashboard` from services.
        - RESTful routes are great for describing actions taken through the API, but they begin to break down for informational routes like this. Most of this comes down to personal preference, but I try to stick with REST as long as I can, and then name routes in the most descriptive way I can think of, and leave comments. A good pattern for naming these routes in your application may emerge as you build out more of them, so pay attention situationally to what the best options are for naming your routes.
- Additional Resources
    - ****Going Further:****
    • A good **[reference](https://www.dofactory.com/sql/left-outer-join)** for join syntax from DoFactory.
    • A cool **[tool](https://sql-joins.leopard.in.ua/)** for visualizing SQL joins with syntax.
    • Another **[tool](https://blog.codinghorror.com/a-visual-explanation-of-sql-joins/)** for visualizing SQL joins syntax for good measure.
    • A **[resource](https://www.moesif.com/blog/technical/api-design/REST-API-Design-Best-Practices-for-Sub-and-Nested-Resources/)** for nested REST routes.
    • Another **[resource](https://docs.universaldashboard.io/rest-apis)** for deep diving into REST routes.**NEXT**
- Normalization in Databases.
    - Check [here](https://www.guru99.com/database-normalization.html).

## Additional Material for SQL, NodeJS, and JS.

- ****[10 JavaScript concepts every Node.js developer must master](https://www.infoworld.com/article/3196070/10-javascript-concepts-every-nodejs-developer-must-master.html).**
- **[Debugging a NodeJS Express API in VS Code Debugger](https://www.moesif.com/blog/technical/debugging/Debugging-a-Node-JS-Express-API-in-VS-Code-Debugger/)**
- ****[Top 11 Node.js security best practices](https://blog.sqreen.com/nodejs-security-best-practices/)****
- ****[Introduction To Advance SQL Interview Questions And Answers](https://www.educba.com/advance-sql-interview-questions/)****
- ****[50 SQL Interview Questions and Answers for 2022](https://www.guru99.com/sql-interview-questions-answers.html)****

## API Documentation && ERD For Database Schema.

- Check [these](http://techslides.com/top-10-free-templates-for-api-documenation) packages rather than documenting your API manually without any aesthetics.
- A [blogpost](https://blog.logrocket.com/documenting-your-express-api-with-swagger/) about documenting API with swagger.
- A cool tool to be used for ERD is [ERDPLUS](https://erdplus.com/).