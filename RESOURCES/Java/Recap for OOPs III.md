# Relationships
- has a
- is a -  Inheritance 
- uses a

## Association
Uses a relationship
- Weakest form relationship
- eg. Driver and a car. Here driver doesn't necessarily have car. Hence here instance variable not needed.
- When needed it uses an instances of dependent object. But doesn't always need it.
- That is parent doesn't need child to be instantiated.


## Composition
Very strong relationship. If a human dies, heart wont exist. There is a strong dependence on existence relationship.
- Has a relation-ship


## Aggregation
Has a relationship
- There is no strong relationship where if parent dies also child dies. Hence weak relationship
- Composition
- Aggregation 
	- Differentiating factor is life cycle dependence.
		- eg. List of students in cohort. Then if cohort dies, then individual students don't die.
- One class had instance variable of child class.


# Design Principles
Ideal guidelines which should be followed.
- extensible : can be reused 
- modular : structured
- simple and easy 
- robust

## SOLID Principles
- Single Responsibility
	- Each class should have only 1 reason to change. That is it should have one functionality. One functionality doesn't mean one function. This applies to only classes as interfaces anyway don't have implementation.
- Open Closed Principles
	- Valid when supporting more things with existing features, doesn't also support adding new functionality as then modification will be needed.
	- Classes are open to extension but closed for modification. If we want to add functionality, extend the class instead of modifying it. Hence to follow this, we need to follow Leskov Substitution Principle.
		- Why follow Leskov?
			- As to achieve modularity, we need abstraction. And that is achieved by using interfaces / abstract classes. But when we do that, all child classes should implement the functionalities defined by parent class and this is what Leskov demands.
- Leskov Principle
	- Substitute child class with parent class without breaking the code. Hence child implement everything of the parent. This "implementation" is honouring the contract.
- Interface Segregation Principle
	- Only implement what they absolutely need. Hence we violate Leskov if not followed.
- Dependency Inversion
	- 
They are all cross related.


# Design Patterns
Real world solutions using design principles to known problems


