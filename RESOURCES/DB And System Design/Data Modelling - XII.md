
# Introduction
Continuation of Schema Design


# Cardinality
When two things are related to each other, how many of one type are associated with how may of the other type.

eg. 
- Student  (1) -> Batch **(1)**
- Student **(N)** <- Batch (1)
then student to batch (n:1)

Types of cardinality
- Monogamy (1:1)
- Many to Many (n:n)
- One to Many 
- Many to One

## How to Represent Cardinality in Tables

- 1:1 
	- one record can store reference of the other record in other table. Thus either can own the relationship. 
	- Also sometimes different one-one table maintained, based on use case such as very sparse or very detailed info about the relationship
-  1:n OR n:1
	- The reference of the one side is put in the table of the many side. This avoid redundancy in table when done in this way.
-  n:n
	- Create a join table, where we have id of both the tables to show relationships


