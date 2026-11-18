# Introduction
A set maintains wether a value exists in O(1) time. We use Has-Sets in java for this.

# Problems
- [Valid Sudoku](https://leetcode.com/problems/valid-sudoku/)
	- Concepts : #Arrays #Matrix #Hash-Table 
	- Approach : We create three functions, to validate each of the rows, columns, and then grids. In each function we use a set to see if we are encountering a duplicate element. We also have to ignore the entries if its '.' cause it represents empty cells. At any point if its a duplicate entry we return false and according return false as result. Or else we return true;
	- Status : Solved
