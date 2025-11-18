Pillars -  Encapsulation, Inheritance, Polymorphism, Abstraction

SOLID is how to apply OOPs to code.

# Encapsulation 
Bundling data and members together into single unit called class.
Access modifiers helps with protecting data and hence helps with encapsulation.
- public anywhere
- default is related to packages. Also called package private cause private outside the package
	- even package inside given package (child package) cant use default.
	- there is no concept of hierarchy in package. Package is namespace. Directory is files.
- private isn't accessible anywhere outside class.
- protected comes into picture only in case of inheritance. - Default + Sub-classes outisde packages.

# Inheritance
- Use commonality from parent
- Also gives  ability to take parents structure and then either extend it, or modify it
- This is used to reference to current object.
- Super is used to refer to parent object. Hence there are two objects. One of the parent and one of the child in which the child references parent along with its properties. Hence also super first, as without parent child can't exist
- Programming to interface rather than concrete class is to use parent reference for child classes. Also called loose coupling
- Also parent reference cant access methods of child with different names.
- Multiple inheritance is not supported due to ambiguity as if p1 -> angry when difficulty, and p2--> sad, then what will child do?(Ambiguity)
- In overriding(Later binding), same signature needed. Runtime polymorphism as object not created till runtime and memory allocated. Also called dynamic method dispatch. HOWWWW? For this (different name function) its not able to find itself what function to call as it doesn't know the function. if same name, then it calls the function but object decides implementation and hence called.
	- Also need same privilege.
- Method over-loading, compile time polymorphism. Also called early binding.
- Constructor chaining.
	- Using this to call other constructors defined in the class.
	- Using the constructor of parent using super.


# Abstraction
When we want only finished structure, then no need for unfinished product, which can then be made as abstract as we don't need object of that un-finished product.
- Encapsulation is a way to achieve abstraction
	- This is because the internal details and working is hidden from the world by puting into an object which only exposes the necessary things outside.
- Two other ways - 
	- The way here for abstraction is defining only behaviour and hiding away implementation.
	- Abstract Classes : Can have one or more body-less functions. 
		- Body-less function-> Abstract function, that is implementation not defined. But everyone who inherits it **HAS** to implement it.
		- Cannot be instantiated.
		- Still has constructor so that class inheriting can use the constructor. The constructors only invoked by child class.
	- Interfaces : When we only have methods and not have data members, which are pure behaviour, then we use interface as only classes  can have instance variables.
		- Are called pure abstraction.
		- Default methods are bodied methods. But this can be over-ridden.
		- Also in case of multiple inheritance, we have to -
			- Either override the function if we have default in both / one of the interfaces or don't define default behaviour
		- Note : Private cant be over-ridden.
	- Difference between them is classes can have instance members (shared data), but interfaces are pure abstraction, and only define behaviour.


---

# ✅ 1. **How does the JVM resolve overridden methods internally?**

Java uses a mechanism called the **Virtual Method Table (v-table)**.

### 🔍 What is a v-table?

Each class that has virtual (non-static, non-final) methods gets a table:

- A list of function pointers to its method implementations.
    
- Subclasses override entries in the parent class’s table.
    

### 🧠 Simplified Example

```
class Animal {
    void sound() {}
}

class Dog extends Animal {
    void sound() {}
}
```

Internally:

```
Animal v-table:
  sound → Animal.sound()

Dog v-table:
  sound → Dog.sound()
```

### 🏃 When calling `a.sound();`

- JVM looks at the **actual object’s v-table**, not the reference type.
    
- If `a = new Dog();` → Dog’s v-table is used → Dog.sound() is called.
    

This is why:

> **Method resolution happens at runtime — based on the actual object.**

---

# ✅ 2. Why don’t static, private, or final methods participate in dynamic dispatch?

Because **dynamic dispatch only applies to methods that can be overridden**.

### ✔️ **Static methods**

- Belong to the **class**, not the object.
    
- Resolved at **compile time** using the reference type → static binding.
    

```java
Animal a = new Dog();
a.staticMethod();  // Calls Animal.staticMethod(), not Dog
```

### ✔️ **Private methods**

- Not visible to child classes.
    
- Cannot be overridden.
    
- Resolved at compile time.
    

### ✔️ **Final methods**

- Cannot be overridden.
    
- No need for dynamic dispatch — JVM always knows exactly which method to call.
    

### 📌 Summary Table

|Method Type|Overridable?|Resolved When?|
|---|---|---|
|static|❌ No|Compile time|
|private|❌ No|Compile time|
|final|❌ No|Compile time|
|overridden instance method|✅ Yes|Runtime|

Only **instance methods that can be overridden** use dynamic dispatch.

---

# ✅ 3. Dynamic Dispatch Flow (Step-by-step)

Let’s say:

```java
Animal a = new Dog();
a.sound();
```

### 🔽 **What happens behind the scenes?**

1. **Compiler check (compile-time)**
    
    - Does `Animal` class have a method named `sound()`?  
        ✔️ Yes → compile passes.
        
2. **Runtime check (JVM)**
    
    - JVM checks the **actual object**, which is a `Dog`.
        
    - JVM looks at the **Dog v-table** entry for `sound`.
        
3. **Execute overridden method**
    
    - JVM jumps to **Dog.sound()**.
        

This is why Java is:

> **Compile-time typed, runtime polymorphic.**

---

# ✅ 4. Why dynamic dispatch enables runtime polymorphism?

Because method selection depends on:

- **Object type**, not
    
- **Reference type**
    

This lets you write flexible, open-ended code:

```java
void process(Animal a) {
    a.sound();  // Works for Dog, Cat, Lion, etc.
}
```

You can add new subclasses **without changing existing code**.

This matches:

- **Open/Closed Principle** (open for extension, closed for modification)
    
- **Loose coupling**
    
- **Flexibility & reusability**
    

---

# 🧠 Final Summary (Very Crisp)

### 🔹 Dynamic Method Dispatch

Runs overridden methods based on **object type** at **runtime**

### 🔹 JVM Mechanism

Uses **v-table** lookup for virtual methods

### 🔹 Static/private/final

Not part of dispatch → resolved at **compile time**

### 🔹 Why important?

Enables **runtime polymorphism**, flexible designs, and OOP power

---
