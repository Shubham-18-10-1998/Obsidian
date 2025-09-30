Works with two pointers moving simulataneously to perform a certain function.

## Problems
- [Compare Version Numbers](https://leetcode.com/problems/compare-version-numbers/)
	- Initial Approach : Worked by covert the parts after establishing equality for a sub section first and then returning the next part between '.'. Eg - 1.001 and 1;
		- Here the problem was issues like 1 and 1.001 were treated equally and other parts.
	- Solution : Two pointer approach to go through the version strings and extract each int based on the conditions of problem and comparing them to return the answer. Unequal was solved by using a flag variable to keep value of extracted val as zero if one of the string had ended and the other didnt but also handle the other version subsection just having 0s.
