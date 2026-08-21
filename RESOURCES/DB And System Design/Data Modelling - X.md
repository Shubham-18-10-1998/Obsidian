
# Introduction



Question : Give all employee details who were hired in 2020
- Then we have two queries
	- Select  from Employee where Year(Date) = 2020
	- Select from Employee where date >= 1-1-2020 & date <= 31-12-2020
- If no index on date, both equal
- If index then, first will have no index being used and hence full table scan
- For query 2, we will use index seek if index is there on date.
Thus if index is there on date, then Query 2 is better.

Strings have Full Text Index


# Order By

Question : Select employees by order of salary dec
- Here select parameters, need not have order by parameters.
- Here all rows are first fetched. then sorted, and then we get filter the names.
SO here query based parameters used first to get data, and then projection paramters applied to get needed view.

Here heap sort is used.
Used here, because RAM is heap, and hence heap sort used.

Use External Merge Sort.

# Aggregate Functions

SUM, AVG, DISTINCT, MIN, MAX, COUNT etc.

Select SUM(salary) from employee.

## How do they work?

Full table scan where the value is stored in a temp variable.

Order BY done before Aggregate.

For AVG, we use SUM() and COUNT(), and then SUM()/COUNT()

Note: in aggregate functions, where doesnt work


# Group By
Full table scan followed by hash-aggregation methods.
Hash-Aggregation Method : Maintain some hashed value per group.

If there is an index, then we dont need to have a hash map, we can keep just two variables, as only one kind of values are going to be seen continuously, and not once another data is encountered.

# Having
Where for aggregated values.
**NOTE** : Group BY has to be there for HAVING

Also it doesn't work, because aggregate function values aren't columns, and hence aren't columns which can be compared using where.

SELECT AVG(salary) FROM employees GROUP BY dept_id HAVING AVG(salary) > 50k.

**NUANCES DEPEND ON HOW CODE WOULD EXECUTE IF WE WROTE CODE FOR THE QUERY**