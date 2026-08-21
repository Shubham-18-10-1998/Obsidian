
# Introduction
Types of SQL commands
Lifecycle of SQL commands (Query Lifecycle)

# Types of SQL Commands
4 Types
- DDL: Data Definition Language
- DML : Data Manipulation Language
- DCL : Data Control Language
- TCL : Transaction Control Language
Language : Cause about SQL : (Structured Query Langauge)

## Data Definition Language (DDL)
Concerned about the Schema (Structure)
- Defining the Schema : How the data will be stored (This is Define/Create)
	- What all Columns
	- What are the data-types
	- Constraints for these columns
	- What all tables
	- What are the relationships between them
	- For this we have Create command
- Update the Schema
	- For this we have Alter Command
- Delete the Schema (DELETE is DML Command)
	- For this we have Drop and Truncate 
		- Drop : Schema is also deleted (Doesn't support rollback)
		- Truncate : Only data is deleted

## Data Manipulation Language
Concerned about the Data 
- Helps with CRUD
	- Here Create : Insert command
	- Read : Select command
	- Update : Update command
	- Delete : Delete command
- Print all students with age > 20
	- Select * from Students where age > 20
- Delete all Students
	- Delete from students [where] (where is optional) 

## What is the difference b/w delete & truncate
- Delete (DML):
	- works on data level
	- Removes the complete  data in O(N), where each row is elected and then delete
	- Here rollback is possible
	- Here counter isnt reset for PK
	- Here table isnt changed
- Truncate (DDL)
	- works on schema level
	- Here Drop and Create used
		- Because Table is deleted (Drop) O(1)
		- And then created O(1)
		- Here rollback not possible
	- Here counter is reset for PK
	- Here table id changed

Question : 10B records, where we want to delete 9.8B records, and want 0.2B records 
Answer : 
	- We can copy 0.2B backup and then truncate data. If we have indexing for data, then its faster. Or we can chunking the data, and then sorting. Without this it still has O(N) complexity, and then Delete also has the same complexity.
	- Here still delete might not be good even with indexing, cause O(log(N)) on 9.8B is still slower than O(log(n)) x 0.2B.
	- Even the backup table should be identical to original table, or else there will be latency in indexing in the table again.
	- Ideally the PK is never copied and is system generated, hence no point copying.

## Data Control Language (DCL)
Subset of SQL to give controlled access of data in DB.
Who and What Defined here : Who gets access to what .

Question: Different ppl with different role access. How does this work?
Answer:
	- We can have, User | Roles table, but this is bad cause individual update may fail giving them undue access based on  previous access
	- So we have Roles : Intermediary layer b/w user and Access Level
	- So each user have role, and that role will have level of access. In case reorg, then we change the role capability.

GRANT : granting a specific level of access.
REVOKE : revoking a specific level of access.

These only give table level access (DB level RBAC). So to maintain column level control, we do application level RBAC.

### Stored Procedures
Create a functional query with variables.(Parameterised execution of SQL) READ ABOUT IT.

## Transaction Control Language (TCL)
This is where Begin and End comes into picture . On end we have either Rollback or commit. This is done using WAL + Checkpoints. Safe-points are also allowed to make transactions have checkpoints. (Also have nested query).


# Query Life Cycle
Whenever we write a query -> result recieved , what are the phases it goes through.

## Parsing and Lexical Analysis
Syntactical checking eg. spelling analysis Select, from where etc are verified.
Write keywords and proper structuring. 

## Semantic Analysis
Table names are checked
Column names are correct
Index are correct.
Access control

(Schema level checks)

## Query Optimisation
Brain of the database
It creates multiple execution flows,  For each query there are mutiple paths to execute, and it choose the best path to use.
Example : Data can have multiple indices, then it checks which will be better.

Complex joins also it sees how to optimise, where second table can be indexed to optimise.

## Execution
Here is Select, Order By etc are done

## Fetch and Return
data is stored in hard-disk in pages, and data stored in bytes (is this binary)
Here then we have transformation , that converts the byte to human readable data.

## Actual LifeCycle
Parse -> Validate -> Re-Write -> Optimise -> Execution -> Fetch and Return.

- **Parse** → syntax check
	- This is like a checing your grammar. Are the spelling of keywords correct, etc. This generates the **Parse Tree OR Syntax Tree**
	- This is how the parse tree is
		- SELECT
		 └── name
		   FROM
		 └── employees
		   WHERE
		 ├── department = 'Engineering'
		 └── salary > 100000
	-         SELECT
	       /   |    \
	name  FROM  WHERE
	        |            |
        employees   >
                  /      \
             salary    100000
     This is the parse tree. This is needed becasue
     - Standard internal format for SQL because DB needs structure and this helps it convert Text -> Structured Data
     - Optimisation works on this tree. The examples of transformation are
	     - Push filter earlier
	     - Reorder Joins
- **Analyze/Validate** → tables, columns, permissions
	- Checks if the given columns even exist and if we have the permissions for them.
	- Matching data types is done here.
- **Rewrite** → simplify query
	- Rewrites the query so it has better structure but in equivalent form.
	- Applies **Rule based transformation**. Here
		- Rearranged expressions, 
		- Simplified expressions
		- Covert subqueries -> join (in complex queries)
	- eg:
		- People in Engineering earning > 100K instead of people earning > 100k and in engineering.
- **Optimize** → choose execution plan
	- Here database considers multiples ways to execute the query 
	- Chooses the cheapest one using a cost model.
	- eg.
		- Scan entire table is slow
		- Use index on department = engineering
			- then filter salary > 100k is faster.
	- Its like Google maps having multiple routes but using the cheapest fastest one based on traffic. 
- **Execute** → run plan
	- Here plan executed step by step.
	- Data fetched from disk in memory.
	- eg.
		- Use index on department = engineering
		- filter those rows by salary > 100K
		- Extract name column
	- Here the B-Tree + Memory is used to get the data.
- **Return** → send result










