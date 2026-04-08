
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