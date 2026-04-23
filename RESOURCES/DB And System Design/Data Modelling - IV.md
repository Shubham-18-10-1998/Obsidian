
# Second Normal Form (2NF)

Observed when there is a composite primary key.
Remove any partial dependency on primary key.

stud_id | stud_name | crs_id | crs_name | instr_id | instr_name | office_hrs 
1            | alice            | 1, 2.      | AI, CSE | 1, 2.  | i1, i2 

1NF : 
1 Alice 1 AI 1 i1
1 Alice 2 CSE 2 i2

- Stud_id + Course_id -> Pk
	- Course name can be derived from just course_id 
	- If any non-key attribute can be derived from proper subset of primary key, then its a partial dependency.
	- Problems :
		- Duplication happens
		- Inconsistency Risk

How to do?
1. Create separate table for set of values that apply to multiple records (the value is repeated).
2. Relate these tables with a foreign key.

Thus 

Course
course_id | course_name | instr_id | inst_name 

Here again we have a composite key course_id and instr_id

course_id | course_name | ..

instr_id | instr_name | ...

Student
stud_id | stud_name | .. | crs_id -> 

Here again we have a composite key which needs to be segregated.
Hence we need a join table.

We need a join table only when there is many-many. If there is many-one relationship then many-side owns the relationship.

# Third Normal Form (3NF)

1. Transitive dependency shouldn't be there in the same table.
2. A non key attribute should not help determine an attribute
	- Eg. instr_id helps to determine instr_name 
If you have a non-key attribute determining another non-key attribute, then along with the primar key, they will form a transitive dependency. This is the issue.

## Transitive Dependency 
a -> b -> c ( a determines b OR b dependent on a)
then a->c Given b !-> a

Eg. Employee_id -> Dept_id  (many to one) QUESTION in the END


# ACID Property
These are some guarantees that DB provides.

ACID isn't necessarily transactions.

- Atomicity : All or nothing
- Consistency :
- Isolation : One thing executing independent of another. BUT their execution may/may-not interfere with some centralised data. 
	- Level of Isolations
- Durability : Once change made, it persists forever.

## Transaction 
All or none kind of operation

Assume i have a single data base Then i have a transactions table for credit and debit entries.
Credit one query, and one debit query : Then we have two queries

We ideally want both to run or none to work. This is what transaction does.

Partial Transactions are automatically rolled back.

### Nested Transactions

### Checkpoints 
- Partial commits in the transaction. So everything before a checkpint are commited but after that are reversed.
- In transaction end is the commit







 
