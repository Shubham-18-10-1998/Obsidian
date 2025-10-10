

## High level language & Low Level Language

- High Level Language: Languages which abstract away most of the hardware details.
	- Write Once, Run Anywhere due to compiler or interpreter.
	- Slower than low level due to abstraction.
	- eg. Java, CPP, Ruby, Python
- Low Level Language : Which provide direct control over hardware and is closer to machine code
	- Assembly Language : Symbolic representation of machine code.
	- Machine Code : Binary Code directly executed by the CPU.
	- Platform dependent.


## Java

### Why is Java Popular?
- Platform Independence:
	- Write once Run anywhere (WORA) : Any machine that has JVM can run Java code.
- Multi-Threading
- Object Orientated Programming
- Large Ecosystem with libraries ,  frameworks like hibernate and Spring
- Security
	- Strong memory management, Security manager and sandboxing for applets.

### Java Architecture
- **JDK (Java Development Kit)** : 
	- The full package for developing Java applications. 
	- Includes
		- JRE (JVM plus libraries)
		- Compiler (javac)
		- Debugger
		- Other development tools
	- Used for writing and compiling java code.
- **JRE (Java Runtime Environment) ** : 
	- Helper Libraries etc are provided by JRE. So essentially JVM plus Library Classes
	- Provides runtime environment
	- Note: Does not include tools like compiler (javac).
	- If you are only running Java application JRE is enough.
- **JVM (Java Virtual Machine) ** : 
	- 3It is the engine (abstract machine) that runs java bytecode. It interprets or just-in-time compiles .class files into machine code for the host OS.
	- The JVM is platform dependent.
	- Loads code, verifies code, executes code, manages memory.

              [Your Java Program - .java]
                         |
	             . javac (Compiler)
                         ↓
			   [Bytecode - .class file]
                         ↓
                   ⬇ JVM (in JRE) ⬇
		   . Converts bytecode → Machine code
                         ↓
                 Runs on your machine

file.java on compliling -> file.class(byte-code) -> jvm works on it -> machine code

When javac file.java done, we generate byte-code which is platform independent.
However the byte-code -> JVM (which is platform dependent) -> machine code which is run by CPU is run.

### Why is byte-code (.class) platform independent and JVM platform dependent?
When we compile the java code we generate .class file (byte-code) which is platform independent. This is sources for Java code portability as this byte-code is platform independent as it only needs a JVM to run on any machine and is same for all.

Advantage of .class file (byte-code) is portability as the Java code after compiling, which generates the .class file can run on any OS without changes.. It prevent to let the code run wild on system like native code might. It also reduces OS based bugs.


The JVM which is platform dependent is then used to convert it to the respective machine code which the machine can then execute.

- Analogy : Consider the byte-code to be English which is universally understood(platform independent), and the JVM to be the language translator to convert this English to the language of the respective machines (machine code).


### Difference between compiler and interpreter.
- **Compiler**
	- Converters entire code to machine code in one go. We get an executable file which is then run.
	- Fast execution but takes time to compile first.
	- eg. C
- **Interpreter**
	- The code is read line by line and then executed.
	- No executable is created.
	- Slower to run but easier to debug
	- eg. Python
- Java uses a compiler to convert the Java file to .class file (byte-code) and then JVM is an interpreter/JIT (Just in time) compiler to run the byte-code.
- **Working in Java**
	- The  JVM runs code using the interpreter.
	- JIT detects frequently executed code (hotspots).
	- JIT compiles that code into native machine code.
	- This native code is cached and re-used for better performance.

### Data Types
Container for storing different types of data, and each container is the Data Type.
#### Primitive Data Type
These are provided by Java, and are not objects. There are 8 in Java .They are fast and memory efficient.
byte, short, int, long, float, double, char, boolean.
#### Non Primitive
They aren't built into the language, like primitive data types. They are used to refer to objects.
eg. 
- String : String s = "";
- int[] arr = {};
- Class : Blueprint for creating objects;
- Object : Parent (Root class) for all Java Objects.

One Java file, one public class at most, but multiple classes allowed.
Name of file is the same as the name of the public class.

Why name of class and file also has to be same?
The Reason for this is that JVM loads classes by name which match the filenames.

### Loops
- **For**
	- for(initialisation : condition; update){Loop body}
	- eg. for(int i=0; i<=5; i++){System.out.println("hello);} : This prints hello 6 times;
- **While**
	- while(condition){loop body}
	- Initialisation done separately and update also has to managed inside unlike for where its stated initially itself
- **do-while**
	- do{loop body}while(condition)
	- Executed at-least once;

## Object Orientated Programming

- Class : Template - they occupy nothing on their own
	- Constructor: A special function, name same as class name, no return type used to initialise data members of class.
		- Default : This is the default Java provides on its own;
		- Parametrised : What we write. If we provide this, then default constructor is lost. If we still want it, then we have to add on our own.
		- Copy Constructor : Used to make copy of an object.
			- This helps avoid shallow copy
				- eg. Person p1 = new Person() / Person p2 = p1;
					- Here the p2 is pointing to same object p1, thus p2 is referencing to p1 and this is known as shallow copy.
					- Using copy constructor we create deep copy by creating a new object with different reference.
- Object : the thing created based on class - occupy space

Copy constructor is special case for parametrised constructor?
Yes

### How addresses work ?

---

#### 🔸 Java Code:

```
class Person {
    String name;
    int age;
}

public class Main {
    public static void main(String[] args) {
        Person p = new Person();  // Step 1
        p.name = "Alice";         // Step 2
        p.age = 25;               // Step 3
    }
}
```

---

####  📊 Java Memory Diagram (Stack vs Heap)

```
             +--------------------+        +-----------------------------+
             |      STACK         |        |            HEAP             |
             +--------------------+        +-----------------------------+
             |                    |        |  Person object              |
             |   p ─────────────┐ |        |  ------------------------   |
             |                 └─┼────────►|  name ─────────────┐    |   |
             |                    |        |  age: 25           |    |   |
             |                    |        +--------------------|----+   |
             |                    |                             ▼        |
             |                    |                   +----------------+ |
             |                    |                   |  "Alice"       | |
             |                    |                   +----------------+ |
             +--------------------+                                       |
                                              (All heap memory is GC-managed)
```

---

#### 🧠 What This Diagram Shows:

- Stack:
    
    - Stores the reference variable p, which holds the address of the Person object in the heap.
        
    
- Heap:
    
    - Stores the actual Person object.
        
    - Inside the object:
        
        - name points to a String object ("Alice") stored elsewhere in the heap.
            
        - age is a primitive and stored directly inside the object.
            
        
    

---
### ✅ Key Concepts Reinforced:
- Java stores objects and their instance variables in the heap.
- Reference variables are stored in the stack.
- Strings like "Alice" are also objects, and thus live in the heap.
- Primitive values like 25 are stored directly inside the object, not as references.
---














