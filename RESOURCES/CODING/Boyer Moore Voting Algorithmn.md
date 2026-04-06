# Introduction
Works when an element exists in majority (ie. greater than n/2 times where n is number of elements in total).
The intuition is :
- For every non-majority element in the array, there is 1 of majority.
- So we give -1 for non candidate and +1 for candidate encountered. If count becomes 0, then that element which made the count 0 is the new candidate.
- This works cause ultimately only the majority element will be able to keep the count > 0.

# Problems
- [Majority Element](https://leetcode.com/problems/majority-element/)
	- Approach : Boyer Moores Voting Algorithm
	- Status : Solved.
