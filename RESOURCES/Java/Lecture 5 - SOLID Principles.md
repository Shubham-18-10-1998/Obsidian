# Introduction

Code Ideal Characteristics-
- Readable
- Modular
- Extendable
- Debug
- Less Complex

To achieve this we use design principles such as SOLID, KISS, YAGIN, DRY etc.

Design Pattern is a reusable solution to common problems in software design which offer specific approaches and templates to solve recurring design challenges.

# Difference btw Design Pattern and Design Principle
- With analogy: Good architecture practices like load bearing wall shouldn't be thin and other such stuff is similar to Design Principles which tell us what to ideally do. Where as the Actual design like L-Shaped kitchen etc. ie. the solutions which can be repeatedly re-applied are called deign patterns. eg. - Singleton, Observer, Factory so on.

# SOLID Principles
- ## S : Single Responsibility Principle
	- Meaning each class/ code unit should have only one responsibility and one reason to change.
	- eg. UTIL class has max violation of S principle but here we bunch everything together which is a violation.
	- Benefits :
		- Testing is easier
		- Lower coupling
		- Organisation as smaller well organised classes are easier to search than monolithic ones.
- ## O : Open/Closed Principle
	- All software entities (eg. class, modules) should be open for extension, but closed for modification.
	- eg. If we have payment class which checks everything within in the same class. this is wrong. TO correct this, have an interface which is implemented by each payment type. This way existing isn't affected and new can be tested separately and added.
	- Benefits:
		- Non-Invasive Changes: Allows adding new features or behaviors without modifying existing code.
		- Reduced Risk: Minimizes the potential for introducing bugs or unintended side effects.
		- Abstract Interfaces: Define contracts for behavior, allowing new implementations to adhere to these contracts.
		- Plug and Play: New functionality can be easily integrated by adding new implementations of existing interfaces.
- ## L : Liskov Substitution Principle (LSP)
	- Subtype (derived classes) must be substitute of their base classes without breaking the existing code.
	- Benefits:
		- Leads to code where subclass implementation doesn't lead to situation where one cant implement all methods of super classes in a sensible manner.
- ## I : Interface Segregation Principle
	- Make interface as small and concise (specific) for each class. This reduces coupling between components.
	- Benefits:
		- Doesn't lead to situation where a dependency is made on interface which has functionality which the the current class doesn't need.
- ## D : Dependency Inversion Principle
	- High-level modules should depend on low-level module; both should depend on abstraction. This promotes decoupling of components through abstraction and interfaces.
	- Benefits:
		- Leads to loose coupling. This reduces dependency on the implementing classes and allows the to swapped easily.


When an interfaces inherits from another interface, then it uses extend?