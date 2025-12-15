# Merge Sort
- Split into 2 part recursively till 1 length achieved.
- The merge to get sorted array in backtrack call area from two child smaller sorted arrays.
- Do implementation

## Time complexity
As we go down n steps, and each step the merging takes O(n) as never we have more than n elements, the complexity becomes n * log(N). Hence time complexity is O(nlogn(n)).


# Quick Sort
- find number of elements of smaller than pivot, and swap
- Keep all elements smaller than pivot to left, and larger to right, and to achieve this swap.
- Implementation Learning : 
	- pivot becomes lowerLimit+count instead of count as we are using portion of array where 0 -> lowerLimit.


# Problems
- [Count Inversions in array](https://www.naukri.com/code360/problems/count-inversions_615\)
	- Learnings : 
		- Ensure what is begin compared to what in loop and comparison conditions.
		- If we want to send a value in the sense of pointer that can be manipulated while passing through parameter, use AtomicInteger, AtomicLong etc.
	- Approach : Use the mergeSort (merging logic) to find where the element to the right is smaller than element to the left.
- 


Practice Questions :

https://www.geeksforgeeks.org/problems/merge-sort/1

https://leetcode.com/problems/reverse-pairs/description/

https://leetcode.com/problems/count-of-smaller-numbers-after-self/description/

https://www.naukri.com/code360/problems/count-inversions_615\
Solved

https://www.naukri.com/code360/problems/quick-sort_983625

