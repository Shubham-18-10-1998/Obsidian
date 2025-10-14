- ## Abstraction
	- Means summary/ high-level view of something
	- To use something, we should know how to use it rather than how its implemented.
		- eg. In car, we don't need to how brakes work in a car to use brakes and stop the car.
	- How Is it implemented in classes?
		- We only need to expose functionality of functions, rather than the working of the functionality.
		- eg. When we use getters and setters then its abstraction as we dont need how its done, we just use it to set or get the values.
- ## Encapsulation
	- Purpose of cover 
		- To hold things inside.
		- Protect inside content from outside.
	- In Class, we have access modifiers, and we can control access of my data in class using these data modifiers.
		- eg, public, private, protected
	- Hence we use functions to alter data members, but otherwise data member access is not given directly.
- ## Inheritance
	- Getting something from the parent.
	- This is used to avoid to redundancy, and stored in a common parent.
		- This class which has common things is then parent. And other classes then "extend" the parent class and get them from there.
	- The parent's functions are exposed to children classes also to be used by them.
	- ### super
		- Used to call the parent constructor.
		- If mulitple constructors, then compiler figures out which one to use when super keyword is used.
	- Types of Inheritance:
		- Single Inheritance - One parent -> one Child
		- Multiple Inheritance - Many Parents -> one Child (not possible in Java)
		- Mutli-level -> parent -> parent-child -> child
		- Hierarchial
- ## Polymorphism
	- Many Forms
	- Types
		- Compile Time (Over-loading) : Name can be same, but signature must be different
			- Since which method to be called decied at compile time, overloading is compile time.
			- Function signature - Combination of function name + type of arguments and number(order of arguments also matter). return type is not part of signature.
		- Run Time (Over-riding): Parent and child have same function and name.
			- Child function version is called and this is called over-riding.
			- Student s(s is called reference) = new Student(); (this side is called instance)
				- Reference of parent can receive instance of itself or child class. What function is called depends on instance. Instance allocated at runtime, hence happens at runtime.
			- Because method to be called depends on the instance, and the instance is created at runtime, hence called runtime overriding.

## Access Modifier Table:

|**Modifier**|**Within Same Class**|**Within Same Package (Different Class)**|**Subclass in Different Package**|**Other Classes (Outside Package)**|**Can be Applied To**|
|---|---|---|---|---|---|
|**`public`**|✅ Yes|✅ Yes|✅ Yes|✅ Yes|Classes, methods, fields, constructors|
|**`protected`**|✅ Yes|✅ Yes|✅ Yes (via inheritance only)|❌ No|Methods, fields, constructors|
|**(default)** _(no modifier)_|✅ Yes|✅ Yes|❌ No|❌ No|Classes, methods, fields, constructors|
|**`private`**|✅ Yes|❌ No|❌ No|❌ No|Methods, fields, constructors (not classes)|

Questions : 
Default and No Args constructor is not the same.
abstraction= hide the implementation
encapsulation=protect the data from outside access

Is the class which has the object, does that decide access or the one which the object of child is created

How does function call work and what happens when function is called?

Why parent reference can refer to child instance? Other way possible ? Why/Why not?

GITHUB LINK : https://github.com/himanshubuyerteam/Java_Oct_Batch
