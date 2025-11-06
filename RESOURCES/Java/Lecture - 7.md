
# Introduction
This lecture talks about design patterns.

# Design Patterns

## Builder
- Creational Design Pattern
- Used when we have to make complex objects
	- When a class has many attributes
	- When some are conditional/ optional and some mandatory.
	- Problem is if many paramtres, (n), then 2^N constructors needed.
- Common Use case for builder:
	- Http-request , then many parametres are there. Then we use Builder design Pattern.
	- When we are making a database query
	- Unit Test
- Working of this method :
	- We have a sub-class (nested) and then we initialise fields with reference of of new object. and then that object is returned so class gets reference.
	- DOUBT : how non-initialised done. we have define behaviour? and also whats the use of nested class


## Adapter 
- used to connect to legacy code where two incompatible types are connected
- In eg, different classes have different implementation, and different names. So if we use interface, we use common name function implemented to bridge the gap.
- We use factory to getting specific Adapter Implementation, and then we can use the common implementation indirectly.
- Working of this :
	- We use the adapter to interact with older code without being directly dependent on it.


## Strategy Design Pattern
- Decide on run-time which algo to use.