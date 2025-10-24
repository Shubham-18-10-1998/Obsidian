# Why OOP is followed?
- It enhances code reusability following the DRY principle (Do not Repeat Yourself)
- Improves scalability as interfaces and classes can be extended to increase levels of implementation
- Reduces code complexity by being modular in nature (classes and objects)

- ## Abstraction
	- Means summary/ high-level view of something
	- To use something, we should know how to use it rather than how its implemented.
		- eg. In car, we don't need to how brakes work in a car to use brakes and stop the car.
	- How Is it implemented in classes?
		- We only need to expose functionality of functions, rather than the working of the functionality.
		- Achieved through abstract classes and interfaces
			- They hold the basis of the functionality and blueprint which can be over-ridden (abstract classes) or hold contract for functionality to be implemented (interfaces) without going into the specifics of the implementation.
		- eg. When we use getters and setters then its abstraction as we dont need how its done, we just use it to set or get the values.
- ## Encapsulation
	- Creating a class which encompasses the data members and their functionalities together is encapsulation
	- Purpose of cover 
		- Makes it into one entity with members and functions.
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
		- Multi-level -> parent -> parent-child -> child
		- Hierarchical - One parent, many children.
	- Polymorphic variables that are used to refer to child class objects can be used to invoke functions only present in both child and parent class. They **cannot** invoke a function present only in child class and not in parent.
- ## Polymorphism
	- Many Forms
	- Types
		- Compile Time (Over-loading) : Name can be same, but signature must be different
			- Since which method to be called decied at compile time, overloading is compile time.
			- Function signature - Combination of function name + type of arguments and number(order of arguments also matter). 
				- return type is not part of signature. Neither is access modifiers or parameter names, or throw clauses.
		- Run Time (Over-riding): Parent and child have same function and name.
			- Child function version is called and this is called over-riding.
			- Student s(s is called reference) = new Student(); (this side is called instance)
				- Reference of parent can receive instance of itself or child class (This is called polymorphic variable). What function is called depends on instance. Instance allocated at runtime, hence happens at runtime.
			- Because method to be called depends on the instance, and the instance is created at runtime, hence called runtime overriding.
			- The return type can be co-variants. That is, the return type of the child can be a sub-class of the return type of the parent.
			- This happens due to **dynamic patching** where the **this** reference that an object inherently passes to its function when invoked, is used to decide the implementation that is to be followed.

## Access Modifier Table:

|**Modifier**|**Within Same Class**|**Within Same Package (Different Class)**|**Subclass in Different Package**|**Other Classes (Outside Package)**|**Can be Applied To**|
|---|---|---|---|---|---|
|**`public`**|✅ Yes|✅ Yes|✅ Yes|✅ Yes|Classes, methods, fields, constructors|
|**`protected`**|✅ Yes|✅ Yes|✅ Yes (via inheritance only)|❌ No|Methods, fields, constructors|
|**(default)** _(no modifier)_|✅ Yes|✅ Yes|❌ No|❌ No|Classes, methods, fields, constructors|
|**`private`**|✅ Yes|❌ No|❌ No|❌ No|Methods, fields, constructors (not classes)|

Questions :
Is the class which has the object, does that decide access or the one which the object of child is created




## Why parent reference can refer to child instance? Other way possible ? Why/Why not?
### 🧩 The Core Idea

In Java:

> ✅ A **parent class reference** can refer to a **child class object**,  
> ❌ But a **child class reference** cannot refer to a **parent class object** (without explicit casting).

---

### 🔹 Example

```java
class Animal {
    void eat() {
        System.out.println("Animal eats");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Dog barks");
    }
}
```

Now:

```java
Animal a = new Dog();  // ✅ Allowed
Dog d = new Animal();  // ❌ Not allowed — compile-time error
```

---

### 🔍 Why the First Is Allowed

When you write:

```java
Animal a = new Dog();
```

You’re saying:

> “`a` is an **Animal-type reference**, but it **points to an object** that is actually a `Dog`.”

This is allowed because:

- Every **Dog _is-an_ Animal** (inheritance relationship).
    
- The compiler knows that whatever a `Dog` is, it at least behaves like an `Animal`.
    
- So you can safely call all methods defined in `Animal`:
    
    ```java
    a.eat();   // ✅ Works
    // a.bark(); // ❌ Not allowed (because Animal reference doesn’t know about bark())
    ```
    

This concept is called **upcasting** (casting from child → parent type).

---

### ❌ Why the Reverse Is Not Allowed

When you write:

```java
Dog d = new Animal();  // ❌ compile-time error
```

You’re trying to say:

> “`d` is a Dog, but I’m giving it a plain Animal.”

This is **unsafe**, because **not every Animal is a Dog** —  
you can’t assume that a general parent object has the child’s specific behaviors or fields.

For example:

```java
Animal a = new Animal();
Dog d = a; // ❌ Compile-time error
d.bark();  // What if 'a' wasn’t a Dog? This would crash.
```

That’s why Java forbids this **downcasting** automatically —  
you must **explicitly cast** it and the JVM will verify it at runtime:

```java
Animal a = new Dog();     // Upcast (safe)
Dog d = (Dog) a;          // ✅ Downcast (safe because a is actually a Dog)
```

But if the object is not actually a Dog:

```java
Animal a = new Animal();
Dog d = (Dog) a;  // ❌ Runtime error: ClassCastException
```

---

### 🧠 Analogy

Imagine:

- **Animal** = generic remote
    
- **Dog** = smart remote with extra buttons (like “bark()”)
    

If you hand someone an **Animal reference**, they can only press the **basic buttons** (methods common to all Animals).

Even if the actual object is a **Dog**, the reference doesn’t know about “bark()”.

But if you hand someone a **Dog reference**, Java expects that object to be a Dog — so if you hand it just an Animal, you’re missing buttons (methods), and that’s unsafe.

---

### 🧩 Summary Table

|**Scenario**|**Code**|**Allowed?**|**Why**|
|---|---|---|---|
|Parent ref → Child obj|`Animal a = new Dog();`|✅|Safe (Dog _is-an_ Animal)|
|Child ref → Parent obj|`Dog d = new Animal();`|❌|Unsafe (not all Animals are Dogs)|
|Downcast after upcast|`Dog d = (Dog) a;`|✅|Safe if actual object is a Dog|
|Wrong downcast|`Dog d = (Dog) new Animal();`|❌ (runtime error)|Object not actually a Dog|


## How does function call work and what happens when function is called?
During a function call, a new stack frame is created for the function.

---

### 🧩 **When a Function (Method) Is Called in Java**

Java uses a **call stack** mechanism to manage method calls.  
Every time a function is called, **a new frame (or stack frame)** is created in the **JVM stack memory** to keep track of that method’s execution.

---

### ⚙️ **Step-by-Step Breakdown**

Let’s take a simple example first:

```java
public class Example {
    public static void main(String[] args) {
        int x = 5;
        int y = 10;
        int result = add(x, y);   // function call
        System.out.println(result);
    }

    static int add(int a, int b) {
        int sum = a + b;
        return sum;
    }
}
```

Now let’s see what happens **when `add(x, y)` is called.**

---

####  🧠 Step 1: **Control Jumps to Method Call**

When `add(x, y)` is executed inside `main()`:

- The JVM pauses `main()` at that line.
    
- It prepares to **transfer control** to the method `add()`.
    

---

#### 📦 Step 2: **A New Stack Frame Is Created**

A **stack frame** for `add()` is created in the **call stack**.  
It contains:

|Inside `add()` stack frame|What it stores|
|---|---|
|Method parameters|`a = 5`, `b = 10`|
|Local variables|`sum`|
|Return address|The line in `main()` where execution should resume after return|

So the call stack now looks like:

```
Top of Stack
+-------------------+
| add(a=5, b=10)    |
+-------------------+
| main(...)         |
+-------------------+
Bottom of Stack
```

---

#### ⚙️ Step 3: **Method Body Executes**

- JVM executes statements inside `add()`:
    
    ```java
    int sum = a + b;   // 15
    return sum;
    ```
    
- Local variables (`a`, `b`, `sum`) live **only inside this stack frame**.
    

---

#### 🔚 Step 4: **Return and Pop Stack Frame**

- When `return sum` executes:
    
    - The value `15` is sent back to the caller (`main()`).
        
    - The **stack frame for `add()` is destroyed** (popped off the call stack).
        
    - Control returns to `main()` at the line after `add()` call.
        

The call stack after return:

```
Top of Stack
+-------------------+
| main(...)         |
+-------------------+
Bottom of Stack
```

---

#### ⚡ Step 5: **Execution Resumes in Caller**

Now `main()` resumes with:

```java
int result = add(x, y);  // returns 15
System.out.println(result); // prints 15
```

---

### 🧭 **Visual Summary**

```
main()
  ↓ calls
add(a, b)
  ↓ returns value
main() resumes
```

🧱 **Memory during execution:**

|Memory Area|What’s Stored There|
|---|---|
|**Method Area**|Class code, method definitions, static data|
|**Heap**|Objects created with `new`|
|**Stack**|Local variables, parameters, return addresses for each active method|

---

### 🔁 **Nested / Recursive Calls**

Each new method call adds **another frame** to the stack — even recursive calls.

Example:

```java
void recurse(int n) {
    if (n == 0) return;
    recurse(n - 1);
}
```

Each recursive call creates **its own stack frame**, with a unique copy of local variables like `n`.  
When the base case hits (`n == 0`), calls return in **reverse order**, popping each frame.

---

### 💡 **Important Points**

|Concept|Explanation|
|---|---|
|**Stack frame**|Temporary memory space for each method call|
|**Local scope**|Variables inside a method live only while that frame is active|
|**Call stack**|LIFO (Last In, First Out) structure managing method execution|
|**Return value**|Passed back to caller, then frame is destroyed|
|**Recursion**|Multiple stack frames of the same method can exist simultaneously|
|**StackOverflowError**|Happens when recursive calls overflow the call stack|

---

### 🧠 In Short:

When a function is called in Java:

1. A **new stack frame** is created for that method.
    
2. **Arguments and local variables** are stored there.
    
3. The JVM **executes** the method’s code.
    
4. When it’s done, the **frame is popped**, and control returns to the caller with any return value.
    

---

GITHUB LINK : https://github.com/himanshubuyerteam/Java_Oct_Batch