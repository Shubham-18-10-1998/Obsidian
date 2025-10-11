Dynamic Programming logic is to store little solutions and work on top of them.

Problems:
- [House Robber](https://leetcode.com/problems/house-robber/)
	- Initial Approach : Use dp to aggregate solutions and work on top of the previous iteration.
	- Learning : For this faced the doubt, what is i-1 has the ax val stored as i-2, then the cur is allowed to have i-1 + cur,  but this is handled by the fact that we are taking max of i-2 + cur , i-1 and since i-1 and i-2 have same value, this case is covered.
- [Coin Change](https://leetcode.com/problems/coin-change/)
	- Initial Approach: Iterate through the coins array for each element, and then check clue for vlaue in dp[i-coins[j]] when i - coins[j] is greater than 0;
	- Learning: Cant use negative value initially itself because then min condtion will not work, hence instantiate with INT_MAX.