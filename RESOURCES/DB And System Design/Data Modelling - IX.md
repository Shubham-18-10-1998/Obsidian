
# Introduction
Query Optimisation in query lifecycle

# Query Optimisation
Assume : 
- Department Table
	- department_id | department_name
- Employee
	- employee_id | first_name | last_name | hirDate (YYYY_MM_DD) | salary
- Project
	- project_id | project_name | manager_id

- Question : Fetch Employee_id, first_name, salary
	- Select emp_id, firstName, salary from employee
	- Here can give alias like e, to help seprate same name columns in different tables
	- Proper way :
		- Select e.emp_id, e.first_name, e.salary from employees e 
	- How does it execute ?
		- Data stored in disk (pages) 
		- We have a pointer, which first points to location of table/page 
		- Like in library we have sections, same happens in DB also. It stores meta data about entity_types (Tables) . First in this query, the pointer will point to that location in the disk and then do consecutive page reads.
		- Iterating over the whole tables is called Full Table scans.
		- Full Table is not always the best options
			- Three types of operations : 
				- Memory (CPU memory / registers) -> 10^8
				- IO operations -> 10^5
				- Network -> 10^2  
			- 10^8 operations means that many CPU cycles exisit. One tick of CPY clock is one operation, and that clock ticks 10^8 times in one sec.
			- CPU has its own memory. Secondary memory isnt directly accessible to the CPU
			- For I/O it reduces to 10^5 operations cause a lot of memory gone in setting up the 
			- Any network call which takes 10ms is best 
			- Then what happens if table is distributed across multiple pages single page -> 4kb 
			- Then first partial pages bought from secondary to CPU
			- Full scan on those pages to get full data from then, then we again fetch new page and process repeats.
			- Therefore Full Table Scan becomes inefficient when data is huge.

## Indexing
They help to locate items better like in a book. They are created on columns. The indexed tree is Self Balanced (n-ary) tree with values of that column(hashed) which then optimises the search by making it O(log(n))
Query :
	- Create Index <index_name> ON <table_name> (col_name/col_names)
 They are of two types
- Cluster Index : Pre Created by the DB, and this is always on PK.
- Non-Cluster Index : Need to create on DB
 For each index, there is an index_table. 
 Whenever we do a write query (C, U, D), it always modify index table.
 Read Heavy System -> multiple indices
 Write Heavy System -> less / no-indices

Index tables only has that col's data

col.value + reference to the actual page having that data row.
so the hashed value (of the column is put generally) -> we get the age, and then the whole page feched and we do a Full Table Scan

Exception : Clustered Index  -> (index, complete row) stored

Clustered index -> if we do indexed search, then not better as if data only on 1 page, then its worse then Full Table Scan, cause first get page, then in that page again full table scan.

- Question Fetch all columns who have sal > 50k
	- Select (star) from employee e where e.sal > 50k
	- Here we have Full Table Scan
	- Index scan not option
	- Index Seek :
		- Since data is now sorted, for index, and then we can get range using something like binary search.

### Partial Index match

Sorting based on something, if multiple columns, then based on all of them.
So it works based on -> 
	first sorted based on first column, -> then sorted based on second column.

If index on emp_name, sal :
 If select ___ from employees where employee_name = 'Rahul'

Options :
	- Full Table Scan
	- Index Scan : Partial Index, based on order of index. since employee_name first, then we get index scan
	- But, when we do filter based on salary, we cant use partial index from here.
- **Note: Thus order does matter in index. **
- **Thus most frquently used columns be put first in the index**
	


Learn 
Select, order_by, aggregate, joins (Basic Queries)