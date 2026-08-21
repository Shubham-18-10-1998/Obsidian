
# Introduction
Schema Design

# Schema Design

## Schema : 
- Structure of DB
- Metadata : Tables, Cols, Pk, Constraints
- Relationships
- Pictorial Representation

## How to approach a schema design problem?
- Always come up with requirements clearly and note them down to avoid problems
- Pre-Requisite : Always have well defined requirements.

eg. 
1. Airtribe will have multiple batches
2. For each batch, we need to store the name, start month and current instructor
3. Each batch will have multiple students.
4. Each batch will have multiple classes
5. Each class, store name, date & time, instructor of class.
6. For students ->name, grad_year, University name, email, phone_no.
7. Every student has a buddy.
8. A student may move from one batch to another.
9. For each batch s student moves to, the date of starting is stored
10. Every student has a mentor.
11. Every mentor -> name, current company_name
12. Store info about all mentor sessions (time, duration, student, mentor, student_rating, mentor_rating)
13. For every batch, store if its AI batch, FE Batch, DSA Batch.

Thus tables decides
- Student, batch, mentor, instructor, class, mentor_session

![[Pasted image 20260507114014.png]]


### Steps to follow

1. Create Tables 
	1. Find out all nouns in the req.
	2. Once nouns encountered, do we need to store any data related to this noun, if yes then create at table
	3. Naming conventions :
		1. Plurals
		2. snake_case
		3. Attribute names : singular forms
	4. Avoid redundancy and have more consistency by creating a new table, eg. instructor
2. Add Primary Key and other attributes
	1. Each primary key should be a separate ID like UUID, incremental id.
	2. In case of join tables, the joint primary keys can be considered PK.
3. Finalise the relationships and then create entries for them in tables based on cardinality rules.