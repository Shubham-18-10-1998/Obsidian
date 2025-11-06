## Introduction
Works with two pointers moving simultaneously to perform a certain function. 
Characteristics -
- Two pointers or indices
- Determinate condition : Which tells which pointer to move.
- Move the pointers
- Termination Condition

## Problems
- [Compare Version Numbers](https://leetcode.com/problems/compare-version-numbers/)
	- Initial Approach : Worked by covert the parts after establishing equality for a sub section first and then returning the next part between '.'. Eg - 1.001 and 1;
		- Here the problem was issues like 1 and 1.001 were treated equally and other parts.
	- Solution : Two pointer approach to go through the version strings and extract each int based on the conditions of problem and comparing them to return the answer. Unequal was solved by using a flag variable to keep value of extracted val as zero if one of the string had ended and the other didnt but also handle the other version subsection just having 0s.
- [Find All K-Distant Indices in an Array](https://leetcode.com/problems/find-all-k-distant-indices-in-an-array/)
	- Initial Approach : Worked with two loops and aux array. The aux array stored all indices such that arr[index] = key. Then another loop is run to check for all elements if the condition is satisfied.
- [Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/): 
	- Initial approach : Fix one element, and do binary search to find the other element. This does it in O(nlogn)
	- Solution (Two pointer approach) : Take i as 0, and j as n-1. And then if sum less than req, then i++, or if sum > target than j--. This works because if sum greater then for all elements sum would then be greater than target.  Similarly if sum < target then i++ as we have checked the condition already for it being fixed there and checking for smaller  already.
- [Segregate 0s and 1s](https://www.interviewbit.com/problems/segregate-0s-and-1s-in-an-array/)
	- Initial Approach : Use a while loop to find first 1 on left and first 0 on right. Then make num[l] = 0 and num[r] = 1, and then continue.
	- Learnings : We need to consider the condition in while loop of increment / decrement cause this is what handles the condition where swap doesn't happen if already in right place.
- [Apply Operations to an Array](https://leetcode.com/problems/apply-operations-to-an-array/)
	- Initial Approach : Use two pointer approach to swap between non zero and zero occurrence. Start both from left side (ie. index 0) and then keep moving right. If non_zero index less than zero index, then non_zero index ++ or else swap and continue process.
	- Learning: After the swap, don't do anything to indices as now they satisfy condition and will find next occurrence.
