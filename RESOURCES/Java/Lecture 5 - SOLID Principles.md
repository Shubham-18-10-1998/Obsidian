# Introduction

Code Ideal Characteristics-
- Readable
- Modular
- Extendable
- Debug
- Less Complex

To achieve this we use design principles such as SOLID, KISS, YAGIN, DRY etc.

Design Pattern is a reusable solution to common problems in software design which offer specific approaches and templates to solve recurring design challenges.

# SOLID Principles
- ## S : Single Responsibility Principle
	- Meaning each class/ code unit should have only one responsibility and one reason to change.
	- eg. UTIL class has max violation of S principle but here we bunch everything together which is a violation.
	- Benefits :
		- Testing is easier
		- Lower coupling
		- Organization as smaller well organised classes are easier to earch than monolithic ones.
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
- ## I : Interface Segregation Principle
	- Make interface as small and concise (specific) for each class. This reduces coupling between components.
	- Benefits:
- ## D : Dependency Inversion Principle
	- High-level modules should depend on low-level module; both should depend on abstraction. This promotes decoupling of components through abstraction and interfaces.
	- Benefits:
		- 




DOUBT - 
then our main class is violating SRP right?
When an interfaces inherits from another interface, then it uses extend?