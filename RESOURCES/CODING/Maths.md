
- # Problems
- [Palindrome Number](https://leetcode.com/problems/palindrome-number/)
	- Approach : Reverse the numbers and compare reversed number with original umber. If they are equal then palindrome or else not.
	- Learnings : 
		- Initially was comparing all digits, but instead just comparing the number also achieves the goal and doesn't need to individually compare each digit.
		- Optimised. Approach Idea : Can reverse half the number and check for equality with rev or rev/10 (rev /10 helps account odd number of digits in the number).
			- However here also need base condition x % 10 == 0 & x != 0
	- Status : Solved
	- 