Continuous block of memory that stores some homogenous kind of data.

- [Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
	- Initial Approach : 2 For loops, and check every possibility
	- Learning - For Sub-array, the new Element is the max Sub-array if curSum (cumulative max is lesser than 0), or else if curSum > 0, then it can contribute t increase the maxSum sub-array.
- [Two Sum](https://leetcode.com/problems/two-sum/)
	- Initial Approach: Use a hash-Map with index and then sort the hash-map. use two pointers to check sum, if greater then reduce back-pointer and if smaller then increase forward-pointer.
	- Learning : Cant sort hash-map as for sort function in cpp to run, as for sort to work it needs random-access iterator which hash-map (unordered_map) doesn't provide.
		- Hence Use vector of pair of int and then solve it using the same logic. This also resolves issue of duplicate elements in parent array which would cause issue in unordered_map as there key has to be unique.
- [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)
	- Initial Approach: Sort the array and check adjacent indices for same value
- [Count Hills and Valleys in an Array](https://leetcode.com/problems/count-hills-and-valleys-in-an-array/)
	- Initial Approach: Use a prevUniq to keep track of prev non-equal element to compare to find occurrence of hill or valley.