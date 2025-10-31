Works with two pointers moving simultaneously to perform a certain function.

## Problems
- [Compare Version Numbers](https://leetcode.com/problems/compare-version-numbers/)
	- Initial Approach : Worked by covert the parts after establishing equality for a sub section first and then returning the next part between '.'. Eg - 1.001 and 1;
		- Here the problem was issues like 1 and 1.001 were treated equally and other parts.
	- Solution : Two pointer approach to go through the version strings and extract each int based on the conditions of problem and comparing them to return the answer. Unequal was solved by using a flag variable to keep value of extracted val as zero if one of the string had ended and the other didnt but also handle the other version subsection just having 0s.
- [Find All K-Distant Indices in an Array](https://leetcode.com/problems/find-all-k-distant-indices-in-an-array/)
	- Initial Approach : Worked with two loops and aux array. The aux array stored all indices such that arr[index] = key. Then another loop is run to check for all elements if the condition is satisfied.
