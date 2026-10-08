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
- protected comes into picture only in case of inheritance. - Default + Sub-classes outside packages.

# Inheritance
- Use commonality from parent
- Also gives  ability to take parents structure and then either extend it, or modify it
- This is used to reference to current object.
- Super is used to refer to parent object. Hence there are two objects. One of the parent and one of the child in which the child references parent along with its properties. Hence also super first, as without parent child can't exist
- Programming to interface rather than concrete class is to use parent reference for child classes. Also called loose coupling
- Also parent reference can't access methods of child with different names.
- Multiple inheritance is not supported due to ambiguity as if p1 -> angry when difficulty, and p2--> sad, then what will child do?(Ambiguity)
- In overriding(Later binding), same signature needed. Runtime polymorphism as object not created till runtime and memory allocated. Also called dynamic method dispatch. For this (different name function/ child class function) its not able to find itself what function to call as it doesn't know the function. if same name, then it calls the function but object decides implementation and hence called. Thus since objects created at runtime, and then what function to call is decided, its called runtime polymorphism.
	- Also need same privilege.
- Method over-loading, compile time polymorphism. Also called early binding.
- Constructor chaining.
	- Using this to call other constructors defined in the class.
	- Using the constructor of parent using super.
- Note : Refer down for the important constructor related information for inheritance.

# Abstraction
When we want only finished structure, then no need for unfinished product, which can then be made as abstract as we don't need object of that un-finished product.
- Encapsulation is a way to achieve abstraction
	- This is because the internal details and working is hidden from the world by puting into an object which only exposes the necessary things outside.
- Two other ways - 
	- The way here for abstraction is defining only behaviour and hiding away implementation.
	- Abstract Classes : Can have one or more body-less functions. Can have defined functions too
		- Body-less function-> Abstract function, that is implementation not defined. But everyone who inherits it **HAS** to implement it.
		- Cannot be instantiated.
		- Still has constructor so that class inheriting can use the constructor. The constructors only invoked by child class.
	- Interfaces : When we only have methods and not have data members, which are pure behaviour, then we use interface as only classes  can have instance variables.
		- Are called pure abstraction.
		- Default methods are bodied methods. But this can be over-ridden. default is used only when providing body to a method in interface. the default access modifier has no keyword.
		- Also in case of multiple inheritance, we have to -
			- Either override the function if we have default in both / one of the interfaces or don't define default behaviour
		- Note : Private cant be over-ridden.
		- If you want to inherit an interface, then we use extends. to inherit the other interface.
		- If there is ambiguity in default implementations from two interfaces that we are implementing, then we still need to implement it to eliminate the ambiguity.
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


# Java — Constructors, Inheritance & `super()`

## 1. Constructor in a Child Class

When creating a child object:

```java
Child c = new Child();
```

the **parent constructor must execute before the child constructor**.

Conceptually:

```text
Create Child object
      ↓
Initialize object fields with default values
      ↓
Initialize Parent fields
      ↓
Run Parent constructor
      ↓
Initialize Child fields
      ↓
Run Child constructor
```

---

## 2. Implicit `super()`

If a child constructor does not explicitly call a parent constructor:

```java
class Child extends Parent {

    Child() {
        // no super() written
        System.out.println("Child");
    }
}
```

Java implicitly adds:

```java
Child() {
    super();
    System.out.println("Child");
}
```

So **`super()` is still called**, even if we don't write it.

---

## 3. What if the Parent Has No Default Constructor?

If the parent defines **no constructor**, Java provides a default no-argument constructor:

```java
class Parent {
}
```

Effectively:

```java
class Parent {
    Parent() {
    }
}
```

Therefore, this works:

```java
class Child extends Parent {

    Child() {
        // implicit super()
    }
}
```

---

## 4. Important: Defining a Constructor Removes the Automatic Default Constructor

If the parent defines a constructor:

```java
class Parent {

    Parent(int x) {
        // ...
    }
}
```

Java **does not** automatically provide:

```java
Parent()
```

Therefore, this child:

```java
class Child extends Parent {

    Child() {
        // implicit super()
    }
}
```

will **not compile**, because Java tries to call:

```java
super();
```

but `Parent()` doesn't exist.

---

## 5. Explicitly Calling the Parent Constructor

The child must explicitly choose an available parent constructor:

```java
class Parent {
    int x;

    Parent(int x) {
        this.x = x;
    }
}

class Child extends Parent {
    int y;

    Child(int x, int y) {
        super(x);
        this.y = y;
    }
}
```

When:

```java
Child c = new Child(10, 20);
```

the constructor flow is:

```text
Child(10, 20)
      ↓
super(10)
      ↓
Parent(10)
      ↓
x = 10
      ↓
back to Child constructor
      ↓
y = 20
```

Result:

```text
c.x = 10
c.y = 20
```

---

## 6. Parent Constructor Cannot Be Skipped

You cannot avoid the parent constructor and initialize inherited fields directly from the child:

```java
class Child extends Parent {

    Child() {
        x = 10;  // ❌ Doesn't solve the problem
    }
}
```

If `Parent()` doesn't exist, the compiler still tries to insert:

```java
super();
```

before `x = 10`.

The parent constructor **must be invoked first**.

---

## 7. `super()` vs `this()`

|Syntax|Purpose|
|---|---|
|`this()`|Calls another constructor in the **same class**|
|`super()`|Calls a constructor in the **parent class**|

Both must appear as the **first statement** of a constructor.

Example:

```java
class Child extends Parent {

    Child() {
        this(10);      // same class
    }

    Child(int x) {
        super(x);      // parent class
    }
}
```

---

## 8. Key Interview Rules

> **Rule 1:** Every child constructor must eventually invoke a parent constructor.

> **Rule 2:** If `super(...)` isn't explicitly written, Java implicitly inserts `super()`.

> **Rule 3:** If the parent has no explicitly defined constructor, Java provides a no-argument constructor.

> **Rule 4:** Once you define any constructor in a class, Java no longer automatically provides the no-argument constructor.

> **Rule 5:** If the parent has no accessible no-argument constructor, the child must explicitly call an available parent constructor using `super(arguments)`.

> **Rule 6:** The parent constructor executes before the child constructor.