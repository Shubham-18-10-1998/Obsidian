# Relationships
- has a : Composition (If child dies when parent dies)/ Aggregation (If child lives even if parent instance cleared)
- is a -  Inheritance 
- uses a : Association

## Association
**Uses a** relationship
- Weakest form relationship
- eg. Driver and a car. Here driver doesn't necessarily have car. Hence here instance variable not needed.
- When needed it uses an instances of dependent object. But doesn't always need it.
- That is parent doesn't need child to be instantiated.


## Composition
Very strong relationship. If a human dies, heart wont exist. There is a strong dependence on existence relationship.
- **Has a** relationship


## Aggregation
**Has a** relationship
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
			- Why Abstraction is needed ? Because that helps us to not modify code of parent by programming to abstraction.
- Leskov Principle
	- Substitute child class with parent class reference without breaking the code. Hence child implement everything of the parent. This "implementation" is honouring the contract.
- Interface Segregation Principle
	- Only implement what they absolutely need. Hence we violate Leskov if not followed.
- Dependency Inversion
	- High Level modules shouldn't depend on low level modules, but instead both should depend on abstractions
		- High Level - App
		- Low Level - Cloud service. (AWS/Azure etc)
		- Here the app will use a reference to abstraction (Cloud service) which will the point to abstraction be it AWS or azure (Concrete implementations)
	- Injection : Each dependency is then injection. This helps dependency inversion.
	- Only when O , L and I followed.
		- Setter Based Injection
		- Construction Based Injection
		- Field based Injection
They are all cross related.

## Advanced Principle :
- Don't Repeat Code (DRY)
	- Reduce duplications in code.
- Keep it Simple Stupid (KISS)
	- Fail Faster
- You Aren't Gonna Need it (YAGNI)
	- Only keep what is needed or code that will be called.
- Law of Demeter
	- Car -> Engine -> Cylinder
		- Here Car shouldn't interact with cylinder directly 
		- Hence it should interact with engine, Engine should interact with cylinder.
		- Reason : Cause later then if cylinder stops dependence on cylinder, our code will have to change
- Prefer Composition over Inheritance (Behavioural Design Pattern : Strategy Design Pattern)
	- Rigidity : 
		- Parent has functionality. Then all children have to implement it or utilise it.
			- Eg. Duck parent class with swim and walk. Rubber duck doesn't need them
	- Fragility : 
		- Fragile Base class problem
		- If base class changed (implementation for function), then child has to override, then lot of extra modification needed.
	- Lack of Change (Inflexibility): 
		- Inheritance is compile time. Which method called depend on object. Once object created, can't dynamically be changed.
	- Solution 1 :
		- Interface Segregation for functionality
		- Cant use programming to interface as functionalities segregated.
		- Hence Failed
	- Final Solution
		- PREFER COMPOSITION OVER INHERITANCE
		  ENCAPSULATE WHATEVER CHANGES
		- Make behaviour, and then use inheritance for specific variation for each behaviour , and then can compose parent with behaviours.
			- Here run-time injection, as once we create object, we later also have flexibility to change behaviour. No longer restricted. 


## Non-Functional Requirements in Designs
- Coupling
	- The dependency of entities between them.
	- Goal : Strive for as low coupling as possible.
- Modularity 
	- Each functionality broken into simpler pieces.
	- Achieved through separation of concerns.
- Separation of Concerns 
	- Modules should have single responsibility.
- Cohesion
	- Friction-less interaction between entities. They should gel with each other.
	- Goal : High Cohesion
		-  Car 10 times -> Engine 10 times. : Needed
		- Car 10 times -> Engine 7 times -> 3 failures , this shouldn't happen


# Design Patterns
Real world solutions using design principles to known problems

Builder Strategy Adapter


