# Introduction
- Find the best solution at each step and hen move forward.
- Choose local optimum solution which leads to global optimal solution.
- 

# Problems -
- [Maximum Number of Operations to Move Ones to the End](https://leetcode.com/problems/maximum-number-of-operations-to-move-ones-to-the-end/)
	- Approach : Count number of ones before a zero. Once zero encountered increment res by numOnes encountered so far. The reason is cause if ones at end without zero no operation possible to shift back .
- [Jump Game](https://leetcode.com/problems/jump-game/)
	- Initial Approach : Finding if a 0 is encountered, and then returning false.
	- Problem with approach : You could have possibly jumped past the index of 0.
	- Approach : Find the max index you can reach at every index which is max(ind, i + num(i)). That way we can track whats the max index we can reach. Condition breaks when we have an index in array which is greater than max_index.
	- Learnings : 
		- Check if the current stage is reachable first 
	- Status : Solved
- [Rabbits in Forest](https://leetcode.com/problems/rabbits-in-forest/)
	- Approach : Maintain count for each answer. For minimum the number of rabbits of same color can be (answer+1). Hence we use ceiling to find number of groups for each answer and that to res.
	- Learning : 
		- Ceiling : if (rem == 0) , then x/y or else (x/y) + 1
		- (int) Math.ceil((double) dividend / divisor)
	- Status : Solved
- [Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/)
	- Approach : Sort the 2-D array by making pairs
	- Learning : 
		- Sort based on end points because that we are shifting intervals left most to be able to add more towards the right. This logic is what makes minimum removals possible.
		- Arrays.sort(intervals, (a, b) -> a[1] - b[1]);
	- Status : Unsolved
- [Partition Labels](https://leetcode.com/problems/partition-labels/)
	- Approach : Was maintaining two maps start and end map, but that isnt needed
	- Learning : 
		- Need only end map to be able to find an intervals possible last index. If we get to max index, then we can create a partition.
	- Status : Unsolved
- [Jump Game II](https://leetcode.com/problems/jump-game-ii/)
	- Initial Approach : Use a stepCount and maxReach to see where we can reach. However this leads to wrong step-count and optimisation as for each step we need the minimum steps needed to reach there.
	- Approach : Use dp[] to keep track of min steps needed to reach a particular index. and ultimately return dp[n-1].
	- Learnings : 
		- Since all possibilities needed we need to use dp.
	- Status : Solved.
- [Assign Cookies](https://leetcode.com/problems/assign-cookies/)
	- Approach : Sort both the greed and size arrays. Then use two pointer to iterate the two arrays in parallel. if greed is less that size, use the cookie or keep moving forward. Sice its sorted that cookie isn't useable in any other case too.
	- Learnings : Even in the case of running through size array to find cookie, once we find the cookie, we have to raise index of j as now that cookie has been used.
	- Status : Solved


  

  

https://leetcode.com/problems/walking-robot-simulation/description/ 

  

https://leetcode.com/problems/score-after-flipping-matrix/description/