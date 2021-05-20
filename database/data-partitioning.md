# Data Partitioning

## Vertical Partitioning

We can partition our database in such a way that we store tables related to one particular feature on one server.

Issues of this approach:

* We'll still have scale issues when one table contains trillions of records that can't fit in one server.
* Joining two tables in two separate databases can cause performance and consistency issues.

## Range based partitioning

We can store files in separate partitions based on the first letter of the file path, i.e. we save all the files starting with letter 'A' in one partition and those that start with letter 'B' into another partition and so on.

We can even combin certain less frequently occurring letters into one databse partition. 

Issues of this approach:

* Lead to unbalanced servers.

## Hash based partitioning

We take a hash of the object we are storing and based on this hash we figure out the DB partition to which this object should go. For example, we can use the hash of the fileID to determine the partition the file will be stored.

This approach can still lead to overladed partitions which can be solved by using Consistent Hashing.

