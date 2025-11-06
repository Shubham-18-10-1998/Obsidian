
# Introduction
- DRY principle
- KISS principle
- YAGIN
- Association, Composition, Aggregation
- Learner Management System Project

# DRY
- Do not Repeat Yourself
	- Essentially means don't repeat code 
	- Benefits
		- Modular
		- Easy to Reuse
		- Easy to modify
		- Easy to understand / debug

# KISS
- Keep it simple stupid
	- Avoid to many if-else ladder etc to increase complexity

# YAGNI 
- You aren't going to need it
	- Only implement functionality that is needed. Avoid unnecessary complexity and features.

# Association
A lose relationship between objects that are independent and can exist without each other. has a **uses-a** relationship.
eg. Teacher-Student, linked to each other, but can exist without each other. What they mean by exist is relationship like heart and human body where heart exists because of body and cant exist without it.
- Here there is no ownership.
- A **works with/ uses ** B
- one-one, one-many, many-many

# Aggregation
A specialised form of association representing whole-part relationship where part can exist independently of whole.
- Has a weak ownership
- **HAS a** relation.
- Eg. 
	- Department and employee. Department **has a** employee.
		- Both can exist individually.
	- Library **has a** book
	- Team has players.

# Composition
A strong (whole-part) relationship where part **cannot** exist independently. If whole gets destroyed, then child also gets destroyed. They have **owned** and **lifetime-bound** to parent object.
Eg. 
- Body -> heart
- House -> room

# Project LMS
- Identify the entities
	- Student
	- Teacher
	- Courses
	- Cohort
	- Use ENUM : Set number of values in that.
		- When to have classes and when ENUM?
			- When implementation can be different then different classes.
	- Student and Teacher have common values, then can extend a USER class.
