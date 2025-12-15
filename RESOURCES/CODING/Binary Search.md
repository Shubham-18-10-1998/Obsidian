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
			- Also condition that arr[start] < arr[mid], then start = mid+1 is wrong, cause it ignores the case where k = 0 scenario.
		4.) Relation to Binary Search:
			- We find condition for element by comparing with given element. Here the condition is its lesser than both neighbouring elements.
			- We choose a condition to discard one half of the array, here the condition is to go to the unsorted half of the array.
		5.)Note : Here end = mid and not mid-1 as the smaller element which is arr[mid] could be the smallest element too!
- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)
	- Learnings : 
		- Use the learnings of previous problem to understand how one part is sorted and other isn't, and how that affects the location of the element wrt to others.
		- Use nums[start] == target and nums[end] == target to find if the element has been found as these are discarded in subsequent iterations.
		- Alternate Approach : Learnt from video that since we know how to find min. index in rotated array (which is the number of rotations clockwise), on either side we have two sorted arrays on which we can subsequently apply standard Binary Search. 
- [Search in an almost Sorted Array](https://www.geeksforgeeks.org/problems/search-in-an-almost-sorted-array/1)
	- Current Thinking:
		- Compare with the element that ind+1, ind and ind-1, cause all elements otherwise are sorted to at max a index of (ind+1)%n, and then use modulo function.
- [Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/)
	- Approach : Create an exhaustive list of all the hrs taken to finish all piles from speed 1 to max(piles) cause cant eat more than 1 pile in a hour. Hence going for a speed faster than that is no use. Then as the hrs taken array is descending sorted, can use binary search to find minimum speed such that hrs <= h.
	- Learning : Don't need to create an auxiliary array to store the results as they are only needed during comparison. Hence get function value and use as otherwise memory exceeded encountered and also there is no use to store all values as many wont even be used.
- [Find Peak Element](https://leetcode.com/problems/find-peak-element/)
	- Key point : nums[i] != nums[i+1];
	- Approach : use binarySearch as multiple value allowed and have to give one of them
	- Learnings : 
		- Say cur = nums[mid], prev = nums[mid-1], next = nums[mid+1], then we have four cases
			- cur > prev && cur > next : This is then an answer
			- cur > prev && cur < next : Here we put start = mid +1 as we have to go towards the larger value because 
				- either next > that its subsequent next , then its a peak or else its lesser than it next and even if this trend continues, then the last element will be the peak.
			- cur < prev && cur > next, then we go end = mid - 1, that is the larger value with same logic as above.
			- cur < prev && cur < next : Here we can go to any direction as we are gurranteed a peak in both halves.
- [Aggressive Cows](https://www.spoj.com/problems/AGGRCOW/ )
	- Approach : Sort the input stalls. Then our search space for gaps becomes 1 to value stalls[len-1] - stalls[0]. We then do a binary search in this search space such that is given gap valid by starting with index 0 as one cow and trying o place cows in stalls with gap >= curGap. if yes, the return true and try finding an ever greater value by continuing the search with start =mid+1. Else gap is greater than we can accommodate all cows, hence end = mid-1.
- [Magnetic Force Between Two Balls](https://leetcode.com/problems/magnetic-force-between-two-balls/)
	- Approach : Same as Aggressive Cows
- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)
	- Approach : The minimum element will be in the unsorted part of the array. However we also have the condition that the array may be sorted after n rotations where n = nums.length . Hence we compare nums[mid] < nums[end]. This way if its sorted then also we go to first half and otherwise if its lightly rotated where the first half is unsorted we go there. OR else the second half will be unsorted and we go the second half of the array to continue the search
- [Minimum Number of Days to Make m Bouquets](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/)
	- Approach : Max is the max of bloomDay and min is 1. For each day that we find mid in terms of binary search, we calculate number of bouquets possible to make. If we find a result we continue to search for smaller value and if number of bouquets possible for that day is less than m, we search in the right of mid.
	- Learnings :
		- Increment of i pointer in calculating bouquets should be done carefully to ensure values aren't being skipped.


Class Problems - 


Homework Problems

https://leetcode.com/problems/binary-search/ - Solved

https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/submissions/494934796/ - Solved

https://leetcode.com/problems/search-in-rotated-sorted-array/description/ - Solved

https://leetcode.com/problems/find-peak-element/description/ - Solved

https://leetcode.com/problems/koko-eating-bananas/description/ - Solved

https://www.spoj.com/problems/AGGRCOW/ - Solved

Try :
[https://leetcode.com/problems/text-justification/?envType=problem-list-v2&envId=vi2q1d91](https://leetcode.com/problems/text-justification/?envType=problem-list-v2&envId=vi2q1d91)

