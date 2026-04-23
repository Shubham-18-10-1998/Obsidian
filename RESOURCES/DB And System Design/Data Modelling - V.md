# Introduction
This note talks about ACID properties

# ACID Properties

- ## Atomicity
	- No concept of partial transaction / updates. (Every query is a self contained transaction).
	- So it essentially means, if i run a query, it must execute completely.
	- Say multiple entry : 
		- Select all employee, then multiple entries in WAL, and check-point either on first, or last, not intermediate stages.
	- Eg. UPI transaction
		- a -> a+100, b -> b - 100
		- Different users balance need not be in the same table.
		- There is no concept of DB level transaction scope for inter-DB operation
		- Cross-DB transaction -> not supported out of the box.

- ## Consistency
	- Standard definition is the property of DB to transition from one valid state to another such that all the defined constraints such as balance >= 0 PK< FK not null etc are verified. 
	- DB Consistency are rules Or constraints guaranteed by DB (Rules for each column are followed)
		- Eg. Create Table Users (id int, int age (check age >=21) );
			- The check on age is DB consistency
		- Eg. 
			- Unique
			- Not null
			- check 
			- range 
			- etc.
	- Say two queries
		- A -> a+100
		- B -> b-80
		- This is not an inconsistent scenario, but not in terms on Consistency of DB, these are application level consistency.
		- Hence this isn't violating DB level guarantees.
	- Example :
		- Email Unique in Db
			- We make the application check if email already exists. (This is not DB wala Consistency)
			- We can define UNIQUE constraints on email column (This is C in ACID).

- ## Isolation
	- Multiple transactions can happen concurrently, 
		- But hey must not interfere with each other
		- Even if interference happens it happens as per tolerance level (Isolation Level)
	- Eg. :
		- User A -> x updated from 90 -> 120
		- User b -> y updated from 60 -> 80
			- These can happen concurrently, Does order matter, NO
			- Issue happens when we try to update same row concurrently as part of different transactions.
		- User A -> x updated from 90 -> 120
		- User b -> x updated from 60 -> 80
			- Here Issue can happen
			- Db operations on 2 different rows are always isolated.
			- Concurrent updated/write on same row, then we can have problems.


- ## Durability
	Once DB acknowledges that i have stored data, it persists forever (ideally).

	### How DB ensures once transaction is committed, it persists?
	- They store the data in secondary memory like hard disk or SSD
	- Write Ahead Logs (WAL): Logging Operations in DB sequentially
		- This is a table in the database.
		- Its **Append Only** (No update)
		- Used in DB writes operation (CUD operations)
		- As is only append, its a cheaper operation : In normal operation, we first fetch, and then update. In WAL we just append, so its faster as no fetching.
		- eg . 
			- All data (eg. student table -> DB - Main File)
			- Want to update to C16 ->
				- First make entry to WAL 
					- Initially it will have data like -> Create | Student_name | C14
					- Then also adds entry -> Update | Student_name | C16
					- Then in main Db file update happens.
		- There is something called "checkpoint" -> tells the DB what all operations logged in WAL were executed. 
		- DB executes operations there after.
		- Operations are atomic, can't lose mid operation. 
		- WAL are recurrently deleted.
		- Select query is combination of DB table and WAL. Once we do commit, only then added to DB table.
		- Rollback -> The check-point is skipped to the point currently in case of roll back, so that those intermediate operations are not committed into the main DB table.
		- Note : Writes to main tables only when commit is encountered.
			- Caveat : Every single query is auto-wrapped in a transaction.
		- Working of WAL Corrected:
			- So WAL is to tell us what all from memory has been flushed to disk. So in case of crash, we only have to redo from checkpoint onwards. 
			- Flow
				- We do a query -> changes in memory
				- Added to WAL -> commit successfull
				- This is then flushed to disk in background
				- Periodicallly as data flushed, checkpoint moves accordingly.
	- ### WAL OPERATION
		- #### 🔥 Clean Final Flow (Correct Mental Model)

		##### 🧠 Normal Execution

		1️⃣ Query runs → changes in memory  
		2️⃣ WAL records all changes  
		3️⃣ COMMIT record added to WAL  
		4️⃣ WAL is flushed to disk  
		5️⃣ DB says: “✅ committed”  
		6️⃣ Data pages updated later (background)

		---

		#### 💥 Crash Recovery

		1️⃣ Start from checkpoint  
		2️⃣ Scan WAL  
		3️⃣ If COMMIT found → REDO  
		4️⃣ If COMMIT missing → UNDO

		---

		#### 🧠 Final Correct Model (One Block)

> When a transaction runs, changes are made in memory and recorded in WAL.  
> Before committing, WAL (including the commit record) is flushed to disk.  
> The actual data pages may still be unwritten.  
> On crash, the database uses WAL to redo committed transactions and undo uncommitted ones.  
> Checkpoints only help reduce how much WAL needs to be replayed, not to track transaction state.

---
		#### 🍽️ Simple Analogy (Lock It In)

- WAL = official ledger
- Memory = working desk
- Disk = final storage
- Checkpoint = “I’ve saved progress till here”

	### Why do we need WAL?
	- Append only, so faster, not much latency
	- Helps in transactions