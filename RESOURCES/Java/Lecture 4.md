
# Introduction
This Lecture focuses on Abstract Classes and Interfaces. Other than that it touched on this keyword, final, static along with Diamond Problem.

# Interfaces
Blueprint of classes that contains abstract methods (and constants)
It is a contract of methods (functions). Contract because all the classes with this interface HAVE TO implement all the functions defined within the interface. 

Use of interface : 
- Eg. if car has music system, then we have to hardcode type without interface. This is called **Tight Coupling**.
- However with interface, its reference can point to instance of any class which implements the interface. The function which are implementing should be public. This is **Loose Coupling**.

Important points :
- Interfaces cannot be used to make objects.
- Interfaces are only used to make references and define contract for classes implementing them.
- The function implementation have to public so its know that all the declarations in interface have been implemented.
- Does signature also have to match to signature in interface? 
	- Yes. The signature must match exactly.
		- However for return type the return type is allowed to be sub-class (covariant) of the type defined in the interface.
- Default functions in interface -
	- After Java 8, interfaces are allowed to have method definitions. Have to use keyword default and the functions are public. To use them -> interface_name.super.function_name()
	- For diamond problem, we have to explicitly provide which implementation to use while implementing and to avoid ambiguity error.


Interview Questions:
- Can interfaces have Data Members?
	- Yes, but they are constants. They are constant and static.
		- The reasons for this are-
			- One, they don't have instances to create instance specific variables to store data.
			- The value belongs to the interface and is common to all, and hence shouldn't be changeable via an object, hence constant.
			- Static cause it belongs to interface and isn't instance dependent. 
- Why can they have reference but not instance?
	- eg. List<Integer> al = new ArrayList<>();
		- Here List is interface and ArrayList is class.
- Can Interface have constructor?
	- No, as they never create objects themselves. They only create references to child classes implementing them.


# Abstract Classes
Classes : declaration + definition for functions
Interfaces : Only declaration for functions.

For Abstract Classes some functions can have declaration or declaration + definitions
- Here for only declaration have to write abstract void function_name();
- Used keyword extend itself.

Important points :
- Abstract classes cannot be used to make objects.

Interview Questions:
- Does abstract class have minimum one abstract function?
	- Not mandatory.
- If a class have one abstract function, then should it be abstract class?
	- Yes.
- Can you make object of abstract class?
	- No. One way is to declare function at time of creating object.
- Can we have data members in abstract class?
	- Yes. They belong at instance level of concrete class implementing them. Not constants like in case of interface.
- Can abstract class have constructor?
	- Yes. They have data-members which have instance level values, then the constructor can instantiate them.

# Differences between Abstract Classes and Interfaces

|Feature|**Abstract Class**|**Interface**|
|---|---|---|
|Can have abstract methods?|✅ Yes|✅ Yes|
|Can have concrete methods?|✅ Yes|✅ Yes (via `default` or `static`)|
|Can have constructors?|✅ Yes|❌ No|
|Can hold instance variables?|✅ Yes|❌ Only constants (`public static final`)|
|Inheritance|`extends` (single)|`implements` (multiple allowed)|
|Access modifiers|public/protected/private|Always public (for methods)|
|Multiple inheritance|❌ No (single abstract class)|✅ Yes (multiple interfaces)|
|Use case|Base class with shared state/logic|Common behavior contract|
|Introduced in|Java 1.0|Java 1.0 (enhanced in Java 8+)|

# Use case for interface and abstract classes. 

|Scenario|Use|
|---|---|
|You want to define a **contract** only (no state)|✅ **Interface**|
|You want to **share code + state**|✅ **Abstract class**|
|You want **multiple inheritance of behavior**|✅ **Interfaces (multiple allowed)**|
|You want to enforce **common fields or constructors**|✅ **Abstract class**|

# Multi Level Inheritance
In java, can't inherit from two classes. 
	Diamond problem.
The problem doest exist with interface. a class can implement multiple interfaces.

Interface              
- Only abstract methods (only declarations). However with default methods they also can have.
- no constructor
- No Diamond Problem (helps solve)
- Here data members are static and final(constant)


Abstract Classes
- Can have both. (abstract methods and concrete methods)
- Can have constructor
- Diamond Problem
- Here data members belong to the instance level.

# This Keyword
This refers to the memory address of the object. For every function called of an object, the memory address is always passed and this is  handled by java and automatically handled.

## Important notes-
|Rule|Description|
|---|---|
|`this` cannot be used in **static** context|Static methods belong to the class, not any specific object.|
|`this()` must be the **first statement** in a constructor|Otherwise, compile-time error.|
|`this` always refers to the **object that invoked the method**|Even if multiple objects share the same code.|

## Uses - 
|Use Case|Example|What It Does|
|---|---|---|
|Differentiate instance vs local variable|`this.name = name;`|Resolves naming conflict|
|Call another constructor|`this(10, 20);`|Constructor chaining|
|Pass current object|`obj.display(this);`|Passes current object reference|
|Return current object|`return this;`|Enables method chaining|
|Access members of current object|`this.value`|Emphasizes current instance|
|Not allowed in static context|`static void test() { this.x = 5; }` ❌|No object exists for `this`|

This is always passed as an implicit hidden argument via the JVM to the object so its data fields can handled if needed.

# Garbage Collector
This is java automatically removing this not being used in the heap.

# Static
- Variable
	- Belongs to the class. All object of that class then have that value as same.
- Method
	- To call the function, we need an object. If we want to access without creating object then it has to be made static. It will work even if we create an object and then call the function. Only gives a warning.

## **In Short:**

> - Static members live in the **class’s memory area** (Method Area / Metaspace), not in any object’s memory.
>     
> - The **JVM allocates memory for static fields and methods when the class is loaded**, long before any object is created.
>     
> - All objects share the same static data — one copy per class.
>     
> - Static methods have no `this`, since they operate without an instance.



# Final
- Variable
	- Cannot be modified
- Method
	- Cannot be over-ride.
- Class
	- Cant be inheritance.




# Can abstract classes implement interfaces and vice-versa?
- Abstract classes can implement interfaces. They can also leave some functions in interface implemented so that the child class can then implement them.
- However Interfaces cannot extend abstract classes. This is because interfaces are like behaviour contracts. However classes have concrete structure and implementation.


# How does reference of reference work in objects?

Let’s unpack it carefully, step by step, because it combines two big ideas:

1. **Objects containing other objects** (composition).
    
2. **How those members are accessed and fetched at runtime.**
    

---

## 🧩 Example to Work With

Let’s take this class:

```java
class Student {
    String name;
    Address address;
}

class Address {
    String city;
    String state;
}
```

Now in `main()`:

```java
public static void main(String[] args) {
    Student s = new Student();
    s.name = "Alice";
    s.address = new Address();
    s.address.city = "Delhi";
    s.address.state = "Delhi NCR";

    System.out.println(s.name);
    System.out.println(s.address.city);
}
```

Now let’s see _how this actually works_ inside the JVM 👇

---

## ⚙️ **1️⃣ Object Layout in Memory**

When you write:

```java
Student s = new Student();
```

- A **Student object** is created on the **heap**.
    
- `s` (a reference variable) lives in the **stack** and holds the **heap address** of that Student object (say, `0xA1B2C3`).
    

Inside that Student object:

- `name` is a **reference** to a `String` object (initially `null`).
    
- `address` is a **reference** to an `Address` object (initially `null`).
    

So the layout in memory looks like this:

```
Stack:                     Heap:
s ───────►  [ Student object @0xA1B2C3 ]
               ├── name    : null
               └── address : null
```

---

## ⚙️ **2️⃣ Assigning a String Member**

When we do:

```java
s.name = "Alice";
```

- `"Alice"` is a `String` object stored on the **heap** (and possibly the String Pool).
    
- The field `name` in the Student object now **stores the address (reference)** of that String.
    

So now:

```
s ───────► [ Student object @0xA1B2C3 ]
              ├── name    : ► [ "Alice" @0xD5E6F7 ]
              └── address : null
```

---

## ⚙️ **3️⃣ Assigning Another Object as a Data Member**

When we do:

```java
s.address = new Address();
```

- A new **Address** object is created in the heap (say at `0xB3C4D5`).
    
- The Student object’s `address` field now stores a **reference** to that Address object.
    

Then we assign:

```java
s.address.city = "Delhi";
s.address.state = "Delhi NCR";
```

Each of those again stores **references** to new String objects.

So final memory picture:

```
Stack:
s ─────► [ Student @0xA1B2C3 ]
           ├── name    : ► [ "Alice" @0xD5E6F7 ]
           └── address : ► [ Address @0xB3C4D5 ]
                             ├── city  : ► [ "Delhi" @0xC9D8E1 ]
                             └── state : ► [ "Delhi NCR" @0xF1E2A3 ]
```

---

## ⚙️ **4️⃣ How Retrieval Works**

When you write:

```java
System.out.println(s.address.city);
```

Here’s what happens **step by step**:

1. **`s`** (stack variable) gives the address of the Student object → `0xA1B2C3`.
    
2. The JVM goes to that heap location and reads the `address` field → another address (`0xB3C4D5`).
    
3. The JVM follows that reference to get to the Address object.
    
4. Inside it, it looks up `city`, which is yet another reference → (`0xC9D8E1`).
    
5. JVM follows that to the actual `String` `"Delhi"` and prints it.
    

So the chain is:

```
s  →  Student@A1B2C3
         ↳ address → Address@B3C4D5
                          ↳ city → "Delhi"@C9D8E1
```

Each **dot (.) operator** in Java is basically a **dereference** step that says  
“follow the pointer/reference stored in this field to the next object.”

---

## 🧠 **5️⃣ What’s Actually Stored Where**

|Level|Stored in|Contains|
|---|---|---|
|`s`|Stack|Reference to Student object|
|`Student` object|Heap|References to `name` (String) and `address` (Address)|
|`Address` object|Heap|References to `city` and `state` (Strings)|
|`String` objects|Heap|Actual text data (internally char[] in older Java, `byte[]` in newer)|

---

## ⚡ **6️⃣ Key Concept — Composition and References**

Each object’s data members that are _objects themselves_ **store references** (memory addresses), not actual copies of those objects.

So:

- Java objects don’t _nest physically_ inside each other.
    
- They **link via references** — like a network of pointers.
    

That’s why you can safely share objects between others:

```java
Address addr = new Address();
Student s1 = new Student();
Student s2 = new Student();

s1.address = addr;
s2.address = addr;
```

Now both students point to the same Address object in the heap.

---

## 💡 **In Short:**

> When you retrieve a data member that’s an object (like `s.address.city`),  
> Java follows a **chain of object references** in heap memory,  
> each “dot” (`.`) meaning “dereference this reference to the next object.”

---

### 🧭 **Summary Visualization**

|Expression|Step|What Happens|
|---|---|---|
|`s`|1|Stack variable holds Student object’s heap reference|
|`s.address`|2|JVM reads the address field inside Student (pointer to Address object)|
|`s.address.city`|3|JVM dereferences Address object and reads its city reference|
|`s.address.city.length()`|4|JVM finds String object and calls `length()` on it|

---
However if the data member is a primitive type like integer etc, then it stored directly in the object at the location.


