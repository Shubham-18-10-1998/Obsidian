
# Introduction
High Level Design -> System Design (LLD + HLD)

## Data Modelling
- Data : Any piece of information
	- Can be structured or unstructured
	- What kind of data used on a daily basis? -> A lot of data such as contact etc are used by us daily
- Drawbacks With Data Storing such as Notepad, Excel etc
	- **Inefficiency** : They aren't efficient to retrieve data. When data bloats, time also increases to extract data
	- **Data Integrity** : 
		- Idea for it : All the constraints defined on data schema are met, and shouldn't be mismatching.
			- Eg. adding words to a column where numerical values are needed (eg. marks where someone adds full)etc, makes the data less unusable.
	- **Data Concurrency** : 
		- If multiple people work on same data together, inconsistency can be observed.
	- **Security Issues** :
		- Control what is accessible to different users when all present together.
		- Encryption 
	- Solution to this is DataBase

## DataBase
- **Definition** : Collection of **related** data.
	- Eg. : AirTribe
		- Student.csv
		- Batch.csv
		- Instructor.csv
- Army Base : Has everything related to army, which are related to each other 
	- eg. Officials, Intelligence, Vehicles etc

## Database Management System
A software system that allows efficiently manage database. Efficiently here means without the drawbacks previously mentioned. It ensures and allows :
- CRUD
	- Create
	- Read
	- Update
	- Delete
- Ensures 
	- Data Integrity
	- Data Security
	- Data Concurrency
	- Efficiency

## Operations to Perform on Data using DBMS
Data Structure - organised way to store and retrieve data. (Store data in meaningful way)
- CRUD
	- Create
	- Read
	- Update
	- Delete

## Types of Databases
- **Relational Database** :  Allows you to store data in form of rows and columns (Tables), along with relationship among them when applicable.
	- Rows are records, columns are fields.
	- There is a relation between rows and columns.
	- All relational databases follow ACID properties, but not all ACID properties following databases are relational databases
	- All relational databases have fixed structure, but not all fixed structure databases are not relational. eg. MongoDB
- **Non-Relational Database** : Data not stored in forms of tables
	-  Store in form of key-value pair etc.
NoSQL can also be relational

## Properties of RDBMS
- Relational Databases represent DB as collection of tables, where each table storing info about something. (Entity or Relationship in term of join table)
- Every row should be unique. Here id allows to keep them unique and hence primary key needed.
- A column should have all values of same data-type. Helps with data integrity
- All the values for a cell should be atomic.
	- Atomic : Have single value
- Sequence of columns is not guaranteed by RDBMS. Done because if storage is not continuous, this allows to keep reference to utilise the data storage.
	- Note: MySQL preserves order
- Sequence of rows is not guaranteed
	- Note: MySQL preserves the order.
- Name of every column has to be unique. This helps avoid \ambiguity in store and fetch.




