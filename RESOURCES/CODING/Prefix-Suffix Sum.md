
# Problems- 
- [Number of Ways to Split Array](https://leetcode.com/problems/number-of-ways-to-split-array/)
	- Approach : Get sum of array from 0 to given index . This is defined as prefix sum. Also total sum minus prefix sum is called suffix sum. These can be compared to get values and accordingly update res.
- [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)
	- Approach : Use a suffix array and a prefix array to stores them for each index, then answer for each index becomes suffix x prefix for that index.
	- Learnings:
		- We can further improve by doing one iteration to right by calculating prefix first, in the reverse iteration we use a variable to store suffix prod, and multiply that with the cur value for given index to get answer for that index.
	- Status : Solved
- [Smallest Stable Index II©leetcode](https://leetcode.com/contest/weekly-contest-498/problems/smallest-stable-index-ii/description/)
	- Concepts : #Prefix #Suffix
	- Approach : Maintain a minSuffix array, and maxPrefix array for each index. since its inclusive of the index, accordingly initiate base condition for both arrays and populate them. Since its the smallest index, the first index we find from 0->n is the result and we break out of the loop from there.
	- Optimisation : We can maintain only minSuffix array as for maxPrefix, we can just maintain one variable containing the max value so far.
	- Status : Solved