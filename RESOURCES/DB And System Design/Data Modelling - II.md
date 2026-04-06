
# Data Modelling
Organise the data in a structure such that it is easy to understand and process.

## Need for it
- To store : Model in some format
- Visualise
- Used for processing

# Entities 

## Entity / Entity Value
Any object that exist in the real world
- Virtual : eg. Order
- Real : eg. Product

## Entity Type
Collection of Entities

## Attribute
Properties or behavors that define the entity

### Attribute Types
- Simple : Can exits independently (atomic)
	- eg. name, email
- Composite Attributes : Composed internally of multiple attributes
	- eg. Address
		- State
		- Zip-Code
		- Landmark
- Single Valued : Eg. roll number
- Multi Valued : Eg. email (primary, secondary)
- Derived Attributes : 


Question : One can buy 1kg onion @ 10 and one kg potato @ 20 and the stock for onion is 20kg and 30kg potato

Then : 
- Entity Type : vegetable (Table)
- Entity : (potato & onion) (Row)
- Attributes : stock and rate (Columns) 

If we have to model

id | name | Stock | Price

If we need age, store DOB as this elimates the need for maintenance of age periodically,


Example : 
st_id | roll_no | name | email | city
## Key Attribute
Attributes or group of attributes that helps us uniquely identify an entity.

## Super Key
Cols or combination of columns that help us to uniquely identify a row
Note : Can have redundant values (which don't uniquely identify) also in it.

## Candidate Key
No redundancy in helping to identify uniquely (Can be composite)
eg. st_id, roll_no, name, email, DOB

Super Key is Super set of candidates key, and candidate keys is super set of primary key.

If we have all unique names, and only one null -> then candidate key, but cant be primary key

## Primary Key 
- Any one of the candidate keys
- It has to be unique
- Not null (Not a constraint on candidate key)
- Only one per table
- Ideally is never string, never any attribute is chosen because attributes can be changed overtime (User - generated, Not system generated)
Why is it never changed 
If pk Changes, (index tree changes and this is bad)

If you have to change or can change pk, then its wrong.
Also PK has an implicit index and this is very expensive for string, and faster for numbers.

Primary Key
- Internally
	- DB sorts data by PK
	- All optputs for query as sorted by primary key
	- DB creates index on primary key
- Should be
	- fast to sort on
	- smaller in size (to optimise index reorder)


## Composite Key
Any key using more than one column
Note : All pk, ck, sk can be composite

Class Questions on students DB 
- Which of the following is super key for student
	- {st_id, crs_id}
	- {first_name, last_name}
	- {age, crs_name}
	- {last_name, crs_id}
- Which of these combinations could also be a super key in students table
	- {st_id, crs_name}
	- {first-name, age}
	- {last_name, age}
	- {crs_id, crs_name}
- Given uniqueness of std_id, which is potential super key
	- {std_id, first_name}
	- {std_id, age}
	- {std_id, last name}
	- All of the above


Questions : 
What are Index trees in data
Self balanced binary search tree



