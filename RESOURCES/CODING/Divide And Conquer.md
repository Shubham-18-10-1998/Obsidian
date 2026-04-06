
# Introduction
- Mostly comprises of Binary Search.
- Also encompasses other sorting techniques.

# Thinking Process
- Identify your search space
- Range must be mono-tonic
This should helps us identify where to go, ie. identify new search range.

# [[Binary Search]]

# Why Mid-Point ?
Helps identify search space without bias. Gives equal success - failure bias.

# Time Complexity
O(log(N))

# Problems 
- [Reverse Bits](https://leetcode.com/problems/reverse-bits/)
	- Approach : Take the original number and get remainder by two. This is the LSB. then keep multiplying res by 2 and adding LSB dervied previously before dividing number by 2.
	- Learnings
		- Can use bit manipulation 
			- res = (res << 1) | (n & 1) : This step left shifts by 1 and appends existing LSB.
			- res >>>= 1 : right shifts by 1 always appending 0.
	- Status : Solved
- [Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
	- Approach : We use a curWindow which keep track of the maximum in the current subarray and one res. when iterating through the sub-array, if cur < 0, then cur = nums[i] or we can say cur = max(nums[i], cur+ nums[i]). and then res = max(res, cur). this works because 
		- we want subarray and hence continous. thus we take them together or start at given index and if sum < 0 , then we can start new window from the new index.
	- Status : Solved






