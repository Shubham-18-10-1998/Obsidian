# Introduction
Basic Definition : Function calls itself back in its body.
- This means the whole function body can replace the area where call is being made.
- Space Complexity for RecursivePrint() -> There is a stack maintaining the order of function calls, and hence O(N).


Recursion means to use a repeated call to the same function with some base condition to terminate the call backs.

# Thinking Process
- Define Problem 
- Can i break bigger problem into smaller sub problems.
- Can i represent smaller sub problem solutions in terms of bigger problem (Utilise solution of smaller problem to solve bigger problem)
	- Can i represent the big problem in terms of smaller problem solution.
- What is the smallest problem i can have.
	- Identifying the base condition / termination process : This is what stops from it becoming an infinite call back loop.

# Problems
- [Fibonacci Number](https://leetcode.com/problems/fibonacci-number/)
	- Learning : Since we use fib(n-2) it can jump to negative values as well. Hence we use condition of if(n<=0) return 0;
- [Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)
	- Learning : Base Condition is when you are on step 0 or step 1, as there is only one way to get there. And then the smaller problem break down is prob(n) = prob(n-1) + prob(n-2)
- Print N to 1
	- Learning : Base condition is 0 to return control.
- Print 1 to N
	- Learning : Base condition is index has reached value n
- 






https://leetcode.com/problems/house-robber/description/ (TRY)

https://leetcode.com/problems/climbing-stairs/

https://leetcode.com/problems/fibonacci-number/ (TRY)

Print N to 1

Print 1 to N

https://leetcode.com/problems/longest-common-subsequence/description/

https://leetcode.com/problems/powx-n/description/

**https://leetcode.com/problems/target-sum/description/?envType=problem-list-v2&envId=dynamic-programming**
