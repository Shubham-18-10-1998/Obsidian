# Foreign Key
A key that is used to uniquely identify a row in another table.

Delete of two types
- Soft delete : Mark as Isdeleted = true, but dont remove the entry. 
	- Helps prevent dependent tables to not have orphan records.
- Hard Delete : Completely deleted the entry from DB
	- Cascade operations come to picture

Note : in heavily distrubuted systems, creating FK is discouraged because of problems to data integrity and operations become expensive. Also Sharding done based on some attribute, and this can cause data to be in different area, and joins cant be done in different location tables.

- Maintain Chronolgy os historic address along with current address. Don't bother customer tables
	- In address table, keep all address data, valid_from, valid_to, and a customer id as foreign_key for customer. here for valid_to make for current address, the valid_to as infinite value. Here no explicit isDeleted col. is required, as we need history.

## Cascade
if i delete entry in one table, what happens to other tables which reference this table.
- Has options like
	- Delete
	- Update


# Normalisation
- Main purpose is to reduce data redundancy.
- Also helps to decide, when introducing new data, 
	- New table or New column in existing table.
- Guidelines, not rules.

## Dependency
One attribute can help us identify others -> then its dependent on those attributes.

student_id --> student_name but not vice-versa.
Hence here student name dependent is student_id. But we call it, student_id determines student_name

stud_id | stud_name | crs_id | crs_name | instr_id | instr_name | office_hrs 
1            | alice            | 1, 2.      | AI, CSE | 1, 2.  | i1, i2 

## 1 Normal Form (1NF)
Each column can have only one value. (No multivalued data in any col)

1 Alice 1 AI i1
1 Alice 2 CSE 2 i2

### Why 1NF ?
Lets say each student takes also CS3
In non-normalised 1st we have to cs1, cs2 -> cs1, cs2, cs3
But in non-normalised, we have to create n new rows.

If we ignore read-patterns 

- Instagram : followers list so we have a list of followers
	- u1 -> {u2, u3, u4...}
	- As per 1NF :
		- u1 -> u2, u1 -> u3 ...
- Amazon : All address of given user.
	- u1 -> {ad1, ad2, ....}
	- As per 1NF
		- u1 -> ad1, i1, ad2 ...
 
 If we analyse write patterns (create, update and delete)
 - Storage Perspective
	 - Row has limit on data.
		 - HD has pages in which data is stored. And to fetch one row, we might have to look through multiple pages.
 - Concurrency Purpose
	 - At some time, multiple people will want to follow , for distributed, we have concurrent thread processing. And then one of them might not have its value updated.
Both these solved, by using new row for entry. 

However for amazon use case, same argument doesn't apply.
	- No million address for one person, so one col. not over different pages
	- Even is address update is there, only 1 address updated at a time.

Thus, theoretically we should apply 1NF but not practical in their case.


Questions :
read about fanning
global address book


# Anomalies
Inconsistency / Errors at large caused by poor schema design
(Data redundancy) .This makes write operations problematic, 

### Insert Analomies
- We insert power B1 but no student and instructor alloted
	- there we get null null and count will be one.

### Update Analomily
Employee working for multiple clients where salry is same, and its like
e1 c1 50k
e1 c2 50k

Data of same employee if distributed, then we have to ensure, cross db transaction while update
needed, but this hard to control.

### Delete Anomaly
Lets say i have single entry for (w/o null) for cs3, and i delete the student corresponding to it

then we lose the corresponding course.

