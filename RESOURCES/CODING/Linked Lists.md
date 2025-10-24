Problems - 
- [Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)
	- Initial Approach : Add the value for the node, keep a variable for carry and keep traversing.
	- Learning : 
		- For pointers in cpp
			- *int ptr = 5, means that ptr is variable that stores the address for integer with value 5;
			- An alternate way is, int val = 5, int* ptr = &val, where now ptr holds the address for variable val, which is same as eg. 1 but with additional steps.
		- Initialising each time slows the code drastically.
		- Keep a prev pointer which points to pen-ultimate node, if no carry is there, then prev->next is nullptr, or else cur->val = 1; Cause we constantly iterate to new node to allow to store val respectively, this handles the last node value cases.