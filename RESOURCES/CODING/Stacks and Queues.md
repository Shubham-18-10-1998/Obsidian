# Stacks
- Follows last in first out property.(LIFO)
- Functionalities of Stack
	- Push - Add a object to the top pf the stack
	- Pop/Peek - Remove an object from the top of the stack
	- Top - Just see the top object of the stack
	- isEmpty() - Tells if the stack is empty

## Stack Problems
- [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)
	- Approach : Maintain a stack of opening brackets, and when matching closing found then pop, or else its invalid.
	- Learnings :
		- Can make a map for the values of opening and corresponding closing bracket.
		- For comparing char, stack.peek.equals(char c) to compare the chars.
	- Status : Solved
- [Next Greater Element II](https://leetcode.com/problems/next-greater-element-ii/)
	- Approach : Maintain a stack for values for which we still have to find the net greater value.
	- Learnings :
		- For circular array can just append the array twice and then consider answer for the first n values.
	- Status : Not Solved


# Queues
- Follows first in first out
- Functionalities of Queues
	- Push() - add object to stack
	- Poll() - Removes first element from queue and returns it
	- isEmpty() - just check if queue is empty
	- Peek - tells first element row 
- ## Dequeue
	- Allows adding and removing from both end.

# Questions
-[Min Stack](https://leetcode.com/problems/min-stack/)
- [Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/)
- l[Next Greater Element II](https://leetcode.com/problems/next-greater-element-ii/)
-  [Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/)
- [First Unique Character in a String](https://leetcode.com/problems/first-unique-character-in-a-string/)