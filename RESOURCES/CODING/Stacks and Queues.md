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
		- Also ensure condition : after iterating string if stack is not empty, then not valid and make flag false.
	- Status : Solved
- [Next Greater Element I](https://leetcode.com/problems/next-greater-element-i/)
	- Approach : Maintain a stack to keep track of element whose next larger has to be found. Then iterate through the array nums2. maintain a map with values such that the key value pair is element -> nextGreaterElement. Do this for whole of nums2. Then iterate through nums1 and populate the nums1 array with results from the map.
	- Status : Solved
- [Next Greater Element II](https://leetcode.com/problems/next-greater-element-ii/)
	- Approach : Maintain a stack for values for which we still have to find the net greater value.
	- Learnings :
		- For circular array can just append the array twice and then consider answer for the first n values.
		- Alternatively, we can just use modulo with length to work on the same array and make index go till 2 times length. However since the stack maintains only elements for which greater than element is yet to be found, we add only indices less than length to stack.
	- Status : Solved
- [Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/)
	- Approach : Use a stack to keep inserting integer values of the token by using Integer.valueOf(token). When an operation is encountered, pop() 2 elements, and then evaluate the result, and push it into the stack. The answer is the last element in the stack as in the end only one element will remain in the stack which is the answer.
	- Learnings :
		- As the values are popped in LIFO order, val2 is popped first and then val1 is popped.
		- Deques are apparently faster and used as stacks in modern java.
		- Use switch case for faster code
	- Status : Solved
- [Min Stack](https://leetcode.com/problems/min-stack/)
	- Approach : Use a stack of pair so that we can store the val, min_so_far together. This works because
		- If the element is smaller than existing value, then we get from this element onwards the value being this value.
		- Is the element is larger it uses the same value.
		- When the cur element is popped, elements before it still store the min_element that was min_so_far before this element.
	- Learnings :
		- For another approach, i used the approach of storing min_encountered value twice, once with new min and once with old min so i can recover it. However this isn't allowed cause in worst case it still O(N) extra space. (Decreasing array input to stack so everything stored twice). This isn't optimal cause worst case its still O(N) extra space.
	- Optimal Approach - Use encoded value for storing only the mins encountered by storing their mirror reflection of old_min wrt to new_min.
		- encoded_val = 2 x (new_min) - old_min
		- This ensures that we get a value less than min for there values as stack.peek() when we are popping the new min, and hence we use the formulae to retrieve the  old_min
			- old_min = 2 x (min) - encoded value as we know the min is the value here.
	- Learnings -
		- To covert Long to int we have 
			- .intValue()
			- (int)(long)
	- Status : Solved



# Queues
- Follows first in first out
- Functionalities of Queues
	- Push() - add object to stack
	- Poll() - Removes first element from queue and returns it
	- isEmpty() - just check if queue is empty
	- Peek - tells first element row 
- ## Dequeue
	- Allows adding and removing from both end.

## Problems 
- [Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks/)
	- Approach : We need two stacks to implement a queue. One to insert. to view and pop, we need another so we can FIFO as stack is LIFO and we need to reverse it.
	- Learnings :
		- In case of pop() and peek() we never need to refill insert as its just for adding new element and have to transfer whenever out /viewPop is empty
	- Status : Solved

# Questions
-[Min Stack](https://leetcode.com/problems/min-stack/)
- [Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/)
- l[Next Greater Element II](https://leetcode.com/problems/next-greater-element-ii/)
-  [Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/)
- [First Unique Character in a String](https://leetcode.com/problems/first-unique-character-in-a-string/)