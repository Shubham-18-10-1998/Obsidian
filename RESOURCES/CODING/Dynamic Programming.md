Dynamic Programming logic is to store little solutions and work on top of them.

Problems:
- [House Robber](https://leetcode.com/problems/house-robber/)
	- Initial Approach : Use dp to aggregate solutions and work on top of the previous iteration.
	- Learning : For this faced the doubt, what is i-1 has the ax val stored as i-2, then the cur is allowed to have i-1 + cur,  but this is handled by the fact that we are taking max of i-2 + cur , i-1 and since i-1 and i-2 have same value, this case is covered.
- [Coin Change](https://leetcode.com/problems/coin-change/)
	- Initial Approach: Iterate through the coins array for each element, and then check clue for vlaue in dp[i-coins[j]] when i - coins[j] is greater than 0;
	- Learning: Cant use negative value initially itself because then min condtion will not work, hence instantiate with INT_MAX.
- [Adjacent Increasing Subarrays Detection I](https://leetcode.com/problems/adjacent-increasing-subarrays-detection-i/)
	- Initial Approach : Use two pointer to check for increasing arrays, and then maintain a flag to see if the current sub-array matching condition exists, or else reset flag and continue.
	- Learnings : Initial approach doesn't work, because it could be a single long increasing sub-array, hence use dp to store length on increasing sub-array at all indices. and compare for index i, i+k. If both >=k, the condition for question met.
- [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
	- Initial Approach : Use two pointers to find buy point and sell point. But wasn't able to establish the condition for pointer movement.
	- Learning : After seeing topic as DP, struck that can use minEle so far value, cause stock selling will need minBuyPoint before it.
- 