
# Classes
- Blue Print for an object
- Has Data (instance variables : because available to the whole class object) and then Methods (Behaviours)
- Method - The brackets shows its a function. These are called instance methods.
	- Return Type : What it gives
	- Name :
	- Body : What needs to be done. Also known as scope of a function. Things defined within it are only accessible within it. Hence called local variable.
- **new** is constructor invocation.
- Default constructor provided if custom constructor not provided. The values are provided default values. Once any constructor provided, then default constructor no longer available.

# Object
Real world representation of a class.
- The objects copy of instance variables are localised. hence when one modified others aren't affected.
- Note : Local variables aren't initialised on their own and then give compilation error. Stored on stack.
- Constructor without parameters is default constructor.
- Default value provided when default constructor not defined also because when initialised on heap, default values given while ear-marking the space for object instance variables.
- Instance method can access static variables. Hence doesn't make sense to access static variables via instance methods
- Static variables are initialised even before object are created/initialised. Hence static methods cannot access instance variables / instance methods.
- Static variables are also initialised by default and also without any object
- Constructor can be called inside another constructor via this() but it needs to be the first statement of the constructor

# Main Class
- Comes default. 
- String[] args is command line arguments which can be given to main function.

# Packages
- Grouping things together
- Every class name is recognised by class + package. This is called fully qualified class name
- Package != Directory

# Memory Model Of Java
- Instance variables initialised in the heap at runtime cause objects created exist in heap. Local variables are stored in stack as they are present in the context of the function. They also don't get default values.
- Static Variables are loading phase in runtime. They also get a default value. Cleaned up only when program ends.
- Different from directory as parent package not available by default in children packages.


