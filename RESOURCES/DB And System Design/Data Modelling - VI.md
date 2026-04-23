# Introduction
Continuation isolation

# ACID Properties

- ## Isolation (Continuation)
	- Multiple transaction happen at same time.
	- If operation of two different rows, then isolation doesnt come into play
	- But if they are on the same row, then issue can come. So isolation says they must no interfere with each other.
	- Example :
		- If two reads, then technically its interference but we don't mind it.
		- We are concerned when one of the concurrent operations is UPDATE/DELETE
		- But even in Cases like BOOKMYSHOW:
			- Even read can cause problem cause we might then want to book subsequent.
	- Thus we choose isolation levels which best suits your use case.
	- DB is very CPU intensive : higher you go on isolation levels, Lower the throughput of query 
	
- ### Isolation Level
	- Isolation Levels define that when multiple transactions are executing in parallel, what level of interference can exist among them.
	- These are defined at DB level.
	- #### Read Uncommitted
		- Say we have two transactions
			- t1 both transactions begin, t2 we update price 100->200 but not committed, and t3 > t2 we get read by different txn2, then if we get read by 200, and this is read uncommitted. 
				- Now this can lead to problem when we use that read to make a business decision based on this data . (Leads to Dirty Read : When you read data thats not committed. (never officially existed in DB) ). 
		- Two transactions such isolated that they can read uncommitted writes from each other also. 
		- Problem : This can lead to Dirty Read.
		- Example:
			- Where we want speed of updates :
				- Eg. : B2C where you want to see how products are behaving in sales like Big Billion Sales, then you seeing dirty read of 200 to 500 reads, in comparison with 10 million records. So this okay, and we do this because of real-time data flowing.
	- #### Read Committed
		- Default isolation level provided by SQL Databases
		- If we read, we only read data from main tables (committed data)
		- Definition : Can only read committed data from another transaction allowed
		- Thus it solves Dirty Read
		- Example :
			- If there is a Distributed System. m1 did update, and then it made call to m2, it did some processing and then reads again, and even m1 is continuing processing. Then m1 -> processing old data but after m2 is processing on updated data.
		- Problem : Non-Repeatable Read.
		- Solution to this is object sent to the next machine to maintain consistency.
	- #### Repeatable Reads
		- If you perform N Reads in a transaction we get the same data irrespective of other transaction changing that in between.
		- This is not absolute (Doesn't guarantee always read repeatable.)
		- txn1 -> reads 5 rows at t1. txn2 -> updates one row among them . now at t3 txn1 reads again. But repeatable read ensures we read the old data itself. 
		- This is done by maintaining views from 1st ever read in a transaction. This view is maintained till transaction is completed.(View kinda like temporary variable storing data of table)
		- Limitations :
			- Complex queries tend not to repeat even when isolation level = Repeatable Read
				- Multi-joins, cross-joins, exist/not exist still may not get the data of view
				- Aggregate queries (eg count) we cant create a view out of it. Hence we don't get the repeatable read
		- Repeatable Reads : It doesn't do query hash (output of query is not hashed/saved)
	- #### Serialisable Reads
		- Strict form of isolation, Its as good as two transactions being executed one after the other.
		- Serialisable takes an exclusive lock especially in case of write.
		- Locks
			- Read Lock : 
			- Write Lock (Exclusive Lock) :
Also 
Pessimistic Locking
Optimistic Locking

Database Internals
System Design Interviews
