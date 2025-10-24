# Introduction
If we want to search for an element in an array (number) then we can compare with each element present to find if it matches with given element. This gives complexity O(n) which is linear. However, if this array was sorted we can use the fact that its sorted to speed up the process. This is where Binary Search steps in.
- We use two pointers, start and end to indicate the start of end of window under consideration at the moment. 
- We then calculate a mid pointer which is (start + end) / 2. We then compare this mid with the element we are trying to find.
	- If element == arr[mid] then we return mid to show we have found the element.
	- If ele < arr[mid] then end is made mid-1, as in the sorted array the element cannot be in the window from mid to end, and we can continue the process.
	- If ele > arr[mid], then start = mid+1, as in the sorted array the element doesnt belong in the window comprised of start to mid, and we continue the process.
- As we are halving the window under consideration in each iteration, the complexity reduces to O(log n) with log being log base 2.


# Identification
- If any question has the word sorted, highly likely that the question can make use if binary search. Another concept is binary search on answer.
- The array will be sorted
- In case of order agnostic search, (when sorting order isn't known to be ascending or descending), compare any two elements. 

# Code 
![[Pasted image 20250806105515.png]]

# Problems
- [First and Last Occurrences](https://www.geeksforgeeks.org/problems/first-and-last-occurrences-of-x3116/1):
	- Learnings: Initial approach was to make the mid element a part of the sub-array before continuing the search in the remaining half sub-array. However, this causes the code to fail as, if we don't make the sub-array reduce in size (ie. end = mid-1. instead of end = mid),  we can get stuck in infinite loop. Hence this had to be corrected.
- [Number of occurrence](https://www.geeksforgeeks.org/problems/number-of-occurrence2259/1):
	- Learnings: Use the first Occurrence and Last Occurrence code and learnings here too.
- [Find Kth Rotation](https://www.geeksforgeeks.org/problems/rotation4723/1):
	- Learnings: 
		1.) Use modulo to handle overflows of index and handle arapping back/forward.
		2.) Small changes in condition can greatly affect the code.
		3.) The base was : 
			- index of smallest element is the number of rotations.
			- The smallest element will be such that element before and after it are both greater than the element itself.
			- the sub-array where the (minimum) element exists will be such that, starting element will be greater than the ending element.
		4.) Relation to Binary Search:
			- We find condition for element by comparing with given element. Here the condition is its lesser than both neighbouring elements.
			- We choose a condition to discard one half of the array, here the condtion is to go to the unsorted half of the array.
		5.)Note : Here end = mid and not mid-1 as the smaller element which is arr[mid] could be the smallest element too!
- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)
	- Learnings : 
		- Use the learnings of previous problem to understand how one part is sorted and other isn't, and how that affects the location of the element wrt to others.
		- Use nums[start] == target and nums[end] == target to find if the element has been found as these are discarded in subsequent iterations.
		- Alternate Approach : Learnt from video that since we know how to find min. index in rotated array (which is the number of rotations clockwise), on either side we have two sorted arrays on which we can subsequently apply standard Binary Search. 
- [Search in an almost Sorted Array](https://www.geeksforgeeks.org/problems/search-in-an-almost-sorted-array/1)
	- Current Thinking:
		- Compare with the element that ind+1, ind and ind-1, cause all elements aotherwise are sorted to at max a index of (ind+1)%n, and then use modulo function.
