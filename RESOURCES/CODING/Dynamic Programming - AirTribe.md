
Recursion plus storing partial result to reduce time complexity. 

Basics of recursion applied
- Smaller problems
- Base Condition
- Use smaller problems to solve bigger problem
- Store the solution for the smaller problems so shouldn't be solved again
- check if smaller problem solved
- Based on number of dynamic parameters, we get dimension of the dp array. as each combination of them gives a sub result.
- By default everything made -1. or make it something thats not possible as answer to know if sub problem solved or not.

# Problems
- [Fibonacci Number](https://leetcode.com/problems/fibonacci-number/)
	- Approach : Top-Down approach where we give auxiliary array and instead of recursion we use our auxiliary dp array to fetch results.
	- Status : Solved
- [Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)
	- Approach : Base case is dp[0] = 1, dp[1] = 1. from there dp[i] = dp[i-1] + dp[i-2].
	- Status : Solved
- [Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/)
	- Status : Unsolved
- [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
	- Approach : the comparison we make for getting lowest price so far and then seeing profit is state compression of dynamic programming. The solution is also written as 
		- minSofar = Math.min(minSoFar, prices[i])
		- dp[i] = Math.max(dp[i-1], prices[i] - minSoFar);
	- Status : Solved
- [Coin Change](https://leetcode.com/problems/coin-change/)
	- Approach : Initially tried a sort of greedy approach, assuming the maximum denomination gives lowest coins. I even sorted the array so that lower coins would fill the dp array first. However this is not correct because this isn't the case for given reasons
		- One consider the max coin need not be used the most times for the result which uis what my assumption was. 
			- eg. 13 using 4 and 5 -> 4 + 4 + 5, however my code would not be able to find a solution as it would as 3 would be not possible for me, and first use of 4 would get 5 as impossible.
	- Learnings : It works withy logic what if i use one more coin, then what can i achieve. This helps solves the possibilities of previous values being populated in the best way too.
	- Status : Solved
- [Word Break](https://leetcode.com/problems/word-break/)
	- Concepts : #DynamicProgramming #Trie #DFS 
	- Initial Approach : Initially tried a trie approach for matching.  Created a trie for wordDict. And then i would go through the word s and try matching, via the logic that if match occurs, then we go to root of trie to continue matching, or else no match return false via a DFS of trie. This leads to TLE as in the matching, we split into 2 options, continuing during match to see if other matches after this match are possible too and this leads to exponential increase in calls.
	- Working approach : Use a dp array start to keep track of indices that allow me to start the word. Initially this is only zero. Then we iterate through this array for only indices that have start as true, and match with our wordDict. if during an iteration if word match occurs and we have ind = s.length, then we have a match, and hence we return true from there. else outside the loop we return false.
	- Optimal Approach : 
		- Use a has set with minLength and MaxLength computed. This reduces the waste comparisons of subtring, and hash-set has o(1) lookup, and hence we try using this to find valid start[i] to compute from and then move forward. If in any iteration we get start[s.length] = true, we return true from there.
		- Use a trie, this helps us compare valid substrings, and does this optimally.
	- Status : Solved
- [Target Sum](https://leetcode.com/problems/target-sum/)
	- Concepts : #DynamicProgramming 
	- Approach : As we need to keep track of values reached at each index, and in the number of ways we can reach it, we see that, dp[i][j+nums[i-1]] += dp[i-1][j]. This helps us know the. number of ways we can reach a given value at a given index. Ultimaltely we have to return dp[n][target+1000] cause i maintained 2D array from -1000 to 1000, where -1000 is 0.
	- Optimal Approach : 
		- We can seprate into two subsets, one having positives and one having negatives. Then s1+s2 = sum, and s1-s2=target, then 2s1 = sum+a=target, thus we can use this s1 target sum to find the sum that the posiitves should genearte. This also helps detect early fail, if its not divisible by two then we can return 0. 
		- Also dp[i+num[i]] = dp[i+nums[i]] + dp[i], as this can be be reached in as many ways as the previous could be reached.
		- We iterate from target to 0, so that when we add, we dont re use them.
	- Old Approach :
		- [[Recursion#Problems]] (Target Sum)
	- Status : Solved.
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
- [Counting Bits](https://leetcode.com/problems/counting-bits/)
	- Approach : Use dynmic Programming to calculate the number of 1 bits for an integer and use this to find them for the other. Now lastMajorEven is last even with only 1 1. Ands for odds its dp[i-1] + 1, where as for even it follows the same pattern for dp[i-lastMajorEven] + 1. cause they get filled right to left so.
	- Optimised Approach : Use bit manipulation, doing i>>2 divides the number by 2. And because the increase in similar fashion for number there bits for even will be same as n/2. and then we use i & 1 to fins if its odd and this gives us an additional 1 to add to the value. for the last bit.
	- Learnings :
		- maxLen initially should be 1 as it essentially tells how many bits at max are being used rn for approach solution.
	- Status : Solved
	- 
https://leetcode.com/problems/longest-common-subsequence/description/
https://leetcode.com/problems/longest-increasing-subsequence/description/
https://leetcode.com/problems/longest-common-subsequence/
https://leetcode.com/problems/fibonacci-number/
https://leetcode.com/problems/edit-distance/ (LCS)
https://leetcode.com/problems/house-robber/ (subset)
https://leetcode.com/problems/word-break/description/ (
https://leetcode.com/problems/russian-doll-envelopes/ (LIS)
https://leetcode.com/problems/partition-equal-subset-sum/description/


Dynamic Programming Practice Problems (by pattern):

Longest Common Subsequence (LCS)

Longest Common Subsequence
https://leetcode.com/problems/longest-common-subsequence/

Edit Distance (LCS-based variation)
https://leetcode.com/problems/edit-distance/

Basic Recursion / DP Warm-up

Fibonacci Number
https://leetcode.com/problems/fibonacci-number/

Subset / 0-1 Knapsack Pattern

House Robber
https://leetcode.com/problems/house-robber/

Partition Equal Subset Sum
https://leetcode.com/problems/partition-equal-subset-sum/

String DP

Word Break
https://leetcode.com/problems/word-break/

Longest Increasing Subsequence (LIS) Pattern

Longest Increasing Subsequence
https://leetcode.com/problems/longest-increasing-subsequence/

Russian Doll Envelopes (LIS variation)
https://leetcode.com/problems/russian-doll-envelopes/

https://leetcode.com/problems/climbing-stairs/

https://leetcode.com/problems/house-robber/

https://leetcode.com/problems/fibonacci-number/

https://leetcode.com/problems/maximum-alternating-subsequence-sum/

https://leetcode.com/problems/partition-equal-subset-sum/

https://leetcode.com/problems/target-sum/

https://leetcode.com/problems/coin-change/

https://leetcode.com/problems/coin-change-2/

https://leetcode.com/problems/minimum-cost-for-tickets/

https://leetcode.com/problems/longest-common-subsequence/

https://leetcode.com/problems/longest-increasing-subsequence/

https://leetcode.com/problems/edit-distance/

https://leetcode.com/problems/distinct-subsequences/

https://leetcode.com/problems/longest-palindromic-substring

https://leetcode.com/problems/palindromic-substrings/

https://leetcode.com/problems/longest-palindromic-subsequence/

https://leetcode.com/problems/partition-equal-subset-sum/description/

https://leetcode.com/problems/partition-equal-subset-sum/description/

https://leetcode.com/problems/partition-equal-subset-sum/description/