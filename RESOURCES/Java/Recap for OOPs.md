
# Classes
- Blue Print for an object
- Has Data (instance variables : because available to the whole class object) and then methods (Behaviours)
- Method - The brackets shows its a function. These are called instance methods.
	- Return Type : What it gives
	- Name :
	- Body : What needs to be done. Also known as scope of a function. Things defined within it are only accessible within it. Hence called local variable.
- New is constructor invocation.
- Default constructor provided if custom constructor not provided. The values are provided default values.

# Object
Real world representation of a class.
- The objects copy of instance variables are localised. hence when one modified others aren't affected.
- Note : Local variables aren't initialised on their own and then give compilation error.
- Constructor without parameters is default constructor.
- Default value provided when default constructor not defined also because when initialised on heap, default values given while ear-marking the space for object instance variables.
- Instance method can access static variables.
- Doesn't make sense to access static variables via instance methods. Also static variables are initialised even before object are created/initialised. Hence static methods cannot access instance variables.
- Static variables are also initialised by default

# Main Class
- Comes default. 
- String[] args is command line arguments which can be given to main function.

# Packages
- Grouping things together
- Every class name is recognised by class + package. This is called fully classified class name
- Package != Directory

Questions - 
Can one constructor call another another constructor.
Runtime phases.
