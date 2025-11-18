
# Problems -
- [Maximum Number of Operations to Move Ones to the End](https://leetcode.com/problems/maximum-number-of-operations-to-move-ones-to-the-end/)
	- Approach : Count number of ones before a zero. Once zero encountered increment res by numOnes encountered so far. The reason is cause if ones at end without zero no operation possible to shift back .