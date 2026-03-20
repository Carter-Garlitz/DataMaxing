\---  
title: "SQL Syntax Part I"  
series: "DataMaxing"  
essay\_number: 07  
section: "SQL And Query Construction"  
level: "Beginner"  
tags: \[SQL\]  
last\_updated: 2026-03-20  
\---  
**SQL Syntax Part I**

\---

**Intro**  
	This and the next few essays will serve to bridge the gap in this discourse between theoretical concepts and practical execution in order that a more in-depth discussion on database operations may be conducted. The previous essay (*What Is SQL*) gave an introduction into the roles and uses of SQL. The next few essays will delve into the syntax of the language. There are many aspects of SQL and therefore the discussion will be broken into multiple parts. Each section will be dedicated to a particular aspect of SQL.   
	The sections will be laid out in a logical order. Building on the main focus of this essay series- learning how databases work rather than memorizing particular skills \- it will be constructed such that each section is derived from the previous. In order to facilitate this structure one example will be used throughout. By constructing an ecommerce database system, we will be able to work through each section cohesively. The first section is dedicated to constructing schemas. Without schema there is simply no database. Building off this, the direction will shift to querying data. Finally we will end with security, transaction controls, and activity logging.   
	It is critical to understand that like learning any language simply reading it once will not be sufficient. Only through practice and particularly through active problem solving will the information be converted to memory. This mini-series will conclude with a remark on the best way I have personally seen to convert this information into practical and usable knowledge.   
**Building Schema**   
We have discussed that schema is the heart of the database and has a great impact on its performance characteristics. In practice, there is a lot of planning and consideration before a schema is finalized. This reflects the importance of its construction and thus should be the first step in our construction. However, as this is not the main focus of our discussion we will keep the theoretical explanation brief for the sake of devoting our energies to syntax.   
In our ecommerce example we will track five core entities; customers, products, orders, order contents, and payment method. From these requirements we will derive the tables needed to express them. Our ecommerce database is an example of an OLTP or online transactional processing database. This means the database is characterized by high write throughput, concurrent transactions and strict consistency requirements. Therefore to protect against update anomalies and keep locking to a minimum, a normalized design should be implemented- we will aim for third normal form (3NF). (see *What Is Normalization* for more detail)  
**Data Types**  
Each attribute of a column must be assigned a datatype. There are a wide variety of datatypes available within SQL and they can vary based on the specific database vendor. There are four categories which partition the datatypes; numeric, character, date/time, and boolean. We will move through each partition naming and describing frequently used data types.   
Examples of numeric datatypes are; INT- a signed 4 byte integer, BIGINT- an 8 byte integer, TINYINT- a 1 byte integer, SMALLINT- a 2 byte integer, DECIMAL(p,s)- a fixed-precision numeric value with p total digits and s digits after the decimal (this data type should always be used for monetary values instead of a float datatype), FLOAT- approximate numeric values represented by a floating point value. (\* the exact size and behavior may vary cross vendors)  
Character data types include; CHAR(n)- a fixed length string datatype (always stores n characters and will pad with spaces if necessary), VARCHAR(n)- a variable length string storing up to n character, TEXT- a large character datatype often used for descriptions and comments (can be stored inside the table as a pointer and to a separate location where the text data is being held (more on how and why this happens in a future essay)).   
Date/Time types include; DATE- stores a calendar date in the format YYYY-MM-DD, TIME- stores the time of day without the date HH:MI:SS, DATETIME- stores both date and time. It is important here to be mindful of timezones. Different vendors can handle timezones in different ways therefore it is important to know the specifics of the vendor you are utilizing.   
The boolean data type stores a true, false, and in some vendors null values. These are stored internally as 1 byte or small integers. They are often used for flags, and active/inactive status.  
**Keys and Constraints**  
	The declaration of primary and foreign keys, as well as constraints can be done while creating tables. A primary key can be declared in two ways. The first is viable only for single column primary keys and this is done by simply writing PRIMARY KEY after the attribute data type. The second method can be used to declare multi-column primary keys. After declaring all the attribute names and data types write PRIMARY KEY(column1, column2, …). Similarly there are two methods of declaring foreign keys. The first works for single column foreign keys. Once again after the data type write REFERENCES Table\_name(column\_name). For multi-column foreign keys after all the attributes have been declared beneath them write FOREIGN KEY(column1, column2, …) REFERENCES table\_name(column1\_name, column2\_name, …).   
	Constraints play an important role in data integrity. Not only can they be used to create alternate keys (see essay 4\) but they can also be used to ensure the data entered fits some specified criteria. All constraints can be declared on single columns by writing the key words after the data type just as with key declaration. The UNIQUE constraint does what you would expect and ensures all inserts and updates have a unique entry in this attribute (this will create an index on the attribute when decaled). It can also be written after all the table attributes have been stated and include multiple columns by UNIQUE(column1, column2, …). The NOT NULL constraint will require any inserts or updates to be not null in the attribute specified. UNIQUE NOT NULL can be combined to give the properties of an alternate key (see essay 4). The CHECK constraint is a very dynamic and powerful one within SQL. This is because you create the function which it checks for a truth value. Upon any insert or update the RDBMS will check to see if the function evaluates as true before it allows the write. The syntax looks like this, CHECK (function1 AND (function2 OR function3)...) (see future essay on querying for a discussion on and/or),  once again written after the data type is declared or for functions involving multiple columns, after all columns have been defined.  
**Alter Table**  
	ALTER TABLE is a method by which you can edit, add, or drop columns, change column names, as well as add or drop keys and constraints to an already existing table. The syntax is simple to add any constraint: ALTER TABLE table\_name ADD CONSTRAINT constraint\_name PRIMARY KEY/FOREIGN KEY/NOT NULL/… . When adding any constraint to a table the database will validate all existing rows, therefore if any row breaks the constraint, the alter table statement will fail. To alter columns ALTER TABLE table\_name ALTER COLUMN column\_name TYPE new\_data\_type/ RENAME COLUMN old\_name TO new\_name/ ADD COLUMN column\_name data\_type.   
**CREATE TABLE**  
The CREATE TABLE statement is what is used to- as its name implies- create a table. Within this statement everything regarding the table can be defined (attributes, data types, keys, constraints…)(It is useful here to note that partitions can also be defined in the create table statement tho we will save the discussion and introduction of this for a later essay on indexes.).   
The template for a create table statement looks like this   
CREATE TABLE table\_name(  
	Attribute1 datatype,  
Attribute2 datatype,  
Attribute3 datatype constraint,  
PRIMARY KEY (attribute1, attribute2),  
FOREIGN KEY (attribute3)   
   REFERENCES different\_table(attribute1)  
);  
**Application**   
	Now as a concrete example we will construct the tables within our example database. It is useful for practice to read through each table creation statement and identify the key components.   
CREATE TABLE Customers (  
    customer\_id INT PRIMARY KEY,  
    first\_name VARCHAR(50) NOT NULL,  
    last\_name VARCHAR(50) NOT NULL,  
    email VARCHAR(255) NOT NULL UNIQUE,  
    created\_at DATETIME NOT NULL  
);  
CREATE TABLE Products (  
    product\_id INT PRIMARY KEY,  
    product\_name VARCHAR(255) NOT NULL,  
    description TEXT,  
    price DECIMAL(10,2) NOT NULL CHECK (price \> 0),  
    active BOOLEAN NOT NULL DEFAULT TRUE  
);  
CREATE TABLE Payment\_Methods (  
    payment\_method\_id INT PRIMARY KEY,  
    method\_name VARCHAR(50) NOT NULL UNIQUE  
);  
CREATE TABLE Orders (  
    order\_id INT PRIMARY KEY,  
    customer\_id INT NOT NULL,  
    payment\_method\_id INT NOT NULL,  
    order\_date DATETIME NOT NULL,  
    order\_status VARCHAR(20) NOT NULL,

    FOREIGN KEY (customer\_id)  
        REFERENCES Customers(customer\_id),

    FOREIGN KEY (payment\_method\_id)  
        REFERENCES Payment\_Methods(payment\_method\_id)  
);  
CREATE TABLE Order\_Items (  
    order\_id INT NOT NULL,  
    product\_id INT NOT NULL,  
    quantity INT NOT NULL CHECK (quantity \> 0),  
    unit\_price DECIMAL(10,2) NOT NULL CHECK (unit\_price \> 0),

    PRIMARY KEY (order\_id, product\_id),

    FOREIGN KEY (order\_id)  
        REFERENCES Orders(order\_id),

    FOREIGN KEY (product\_id)  
        REFERENCES Products(product\_id)  
);

\---

\#\# Part of the Series

\<- Previous: \[What Is SQL\](06\_What\_Is\_SQL.md)  
\-\> Next: \[SQL Syntax Part II\](08\_SQL\_Syntax\_Part\_II.md)

From : \[04, 05, 06\]  
Leads to : \[08, …\]

\---