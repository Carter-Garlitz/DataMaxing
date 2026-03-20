\---  
title: "What Is SQL"  
series: "DataMaxing"  
essay\_number: 06  
section: "SQL And Query Construction"  
level: "Beginner"  
tags: \[SQL\]  
last\_updated: 2026-03-17  
\---  
**What is sql**

\---

**Intro**  
A major advantage to utilizing a RDBMS is the layer of abstraction between the user and the data itself. This allows for the database to optimize layout on disk, while supporting accessibility for a wide range of user needs. Most general purpose programming languages such as Python or C are imperative languages. This means you must give specific instructions as to how the computer will execute some process in order to produce the desired result. This however can lead to accessibility problems when attempting to interact with these underlying structures within a database. Structured query language or SQL was developed in the 1970’s and has stood the test of time remaining a titan of the industry and is the primary language used to interact with relational database systems. SQL is the method by which users can read, write, and query data and build schema within the database. In addition SQL has commands to control data accessibility, and control transactions. These aspects form specific subsectors of SQL; DDL (structure), DML (data manipulation), DCL (security), TCL (transactions). SQL solves the accessibility issue by utilizing declarative and set based programming. Being declarative, in SQL the user specifies the desired result and the database engine formulates the algorithm that will retrieve it. Operations in SQL act on entire sets of data rather than individual records, a shift that may feel unfamiliar to programmers accustomed to row-by-row execution.   
 	One of the greatest benefits to the use of a declarative language and SQL in particular is that it can be standardized across vendors. This means that the same language and syntax is used within all of the most common relational database products including; MySQL, PostgreSQL, SQL Server, Oracle, and SQLite. There do exist differences between the databases however this is mostly to provide syntax for capabilities which are unique to the databases themselves, and can be learned quickly and easily.    
**Query Structure**  
	The syntax of SQL is easy to learn as it follows a human language like structure (more on syntax in a later essay). SQL provides a great deal of versatility while following a simple structure. Queries generally follow this format \- data source selection, filtering data, combining tables, aggregating tables then sorting output. Once the query has been run the engine will step in to develop an algorithm which it thinks will best return the results specified(more on the engine in a later essay).   
One difficulty when learning SQL comes from this separation of query structure and engine interpretation. The logical processing order for a query is not the same order in which it is written; The engine does not work in the same order as the written query. This can be a cause of confusion for new programers- particularly those with prior experience in imperative languages- as they will naturally try to write queries in the order the engine will execute them. This however is easy to overcome with practice and once mastered provides a natural ease to query writing not found in imperative languages.   
**Output Structure**  
The output of a query will always be in the form of a table with columns of the data selected and rows being the output of the records. As a beginner to SQL it is important and helpful to keep this in mind when writing queries as it can help to avoid making logical mistakes.   
One of the most powerful results of this tabular output is that query results behave logically as tables themselves. This means you can write queries which select from previous queries, or create columns and entire tables that are the result of a query. This is a very powerful and useful aspect of SQL, particularly for analytics. This feature helps to negate one of the downsides of SQL which is that complex procedural queries can be clunky and hard to manage. By breaking the process into parts, each part can access the results produced by its precursors making the process feel more natural and controllable.   
**Summary**  
	The declarative nature of SQL helps users to interact with the data help within the database in a natural and predictable manner. The same database must be able to operate for both the  transactional needs of small companies and the massive data warehouses of mega corporations. Leaving the underlying algorithmic decisions to the database engine allows for scalability and thread management, thus the operations are optimized to the requirements of the database. Being declarative makes SQL relatively easy to learn for new programmers but may at first seem confusing to those with experience in imperative languages. Understanding the structure of queries and the formatting of their results can help to make the learning process easier. 

\---

\#\# Part of the Series

\<- Previous: \[What Are Keys\](05\_What\_Are\_Keys.md)  
\-\> Next: \[SQl Syntax Part I\](06\_SQL\_Syntax\_Part\_I.md)

From : \[05\]  
Leads to : \[07, …\]

\---
