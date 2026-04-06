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
- [Target Sum](https://leetcode.com/problems/target-sum/)
	- Learning : Can understand it as water trickling down paths, you send water down one path and then it goes down the other, and as its recursive calls to the end, eventually the scenarios that were covered for later indices are recovered for the new scenario of this index(ie. the exploring of possibility happening for positive is also down for negative, cause you come back up the recursive ladder again and then again go down it with new scenario). 
	- Also cant use static variable to keep track as its for the class, and hence either reset it every time before function call or make object with res instance value 0 in constructor and then call recursively the function and run.
- [Find the K-th Character in String Game I](https://leetcode.com/problems/find-the-k-th-character-in-string-game-i/)
	- Learning : Have to type-cast char + int to char again to be made into char. Also since once str length >=k, then it wont change, hence can stop then, instead of doing operation k times.
- [Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/)
	- Approach : use two index variables, and then if for both strings at given index we have same character, return 1 + sub(index1+1, index2+1) or else return max(sub(index1+1, index2), sub(index1, index2+1))
- [Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/)
	- Approach : base case is if n == 0 || n == 1, return n or else we have to return 1 + function(n % Math.pow(2, maxPower)).
	- Status : Solved
- [Permutations](https://leetcode.com/problems/permutations/)
	- Concepts - #Backtracking #Recursion
	- Approach : Make the res a global instance variable. Now we pass to the helper function, an existing list, which has values added before it. We start with empty list, and pass a count for number of numbers the perm contains. If count == nums.length, then we add the perm to res and return or else, we iterate through the array, add the number to a copy of the perm, and pass it to helper again with count+1.
	- Learnings
		- The count at max will be equal to nums.length when all values added to perm, so we should return from there.
		- For backtracking solution, add the value, explore subsets, and then remove the value. This way we optimise by not having to create many auxiliary perm arrays that are not used later.
	- Status : Solved



https://leetcode.com/problems/house-robber/description/ (TRY)

https://leetcode.com/problems/climbing-stairs/

https://leetcode.com/problems/fibonacci-number/ (TRY)

Print N to 1

Print 1 to N

https://leetcode.com/problems/longest-common-subsequence/description/

https://leetcode.com/problems/powx-n/description/

**https://leetcode.com/problems/target-sum/description/?envType=problem-list-v2&envId=dynamic-programming**
