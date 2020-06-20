# SQL vs NoSQL

SQL: relational database store data in tables which are formed in rows and columns. 

NoSQL: 

* key-value
* document
* graph

## High level differences

### Storage

SQL: table

NoSQL: key-value, document, graph.

### Schema

SQL: fixed

NoSQL: dynamic

### Querying

SQL: uses SQL \(structured query language\)

NoSQL: UnQL \(unstructured query language\).

### Scalability

SQL: vertically scalable. Hard to horizontally scale

NoSQL: horizontally scalable.

### Reliability or ACID Compliancy \(Atomicity, Consistency, Isolation, Durability\)

SQL: ACID compliant

NoSQL: sacrifice ACID compliance for performance and scalability.

## Ideal Applications

[https://www.sitepoint.com/sql-vs-nosql-differences/](https://www.sitepoint.com/sql-vs-nosql-differences/)

### Projects where SQL is ideal

* logical related discrete data requirements which can be identified up-front
* data integrity is essential
* standards-based proven technology with good developer experience and support.

### **Projects where NoSQL is ideal**

* unrelated, indeterminate or evolving data requirements
* simpler or looser project objectives, able to start coding immediately
* speed and scalability is imperative.

[https://github.com/donnemartin/system-design-primer\#sql-or-nosql](https://github.com/donnemartin/system-design-primer#sql-or-nosql)

* Rapid ingest of clickstream and log data
* Leaderboard or scoring data
* Temporary data, such as a shopping cart
* Frequently accessed \('hot'\) tables
* Metadata/lookup tables

