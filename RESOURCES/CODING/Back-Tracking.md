
# Introduction
- Similar to recursion
- When call to child completed in recursion, then call goes back to parent. The call back is back-tracking piece. Then can use child's data to evaluate, this is back-tracking.
	- Hence anything after child call in parent function is part of back-tracking.

# When to use?
if you want to explore all possible paths.

# Problems
- [N-Queens](https://leetcode.com/problems/n-queens/)
	- Note : In Java objects passed as reference, not deep copy mades.
	- Approach: Initially in each row we know one queen allowed, then we assume every column and try going from there to see of other queens are fitting. Hence here back-tracking helps to explore all possibilities (all columns in a given row)
		- String builder to make char to string. String builder append. and then stringBuilder.toString().
- [Word Search](https://leetcode.com/problems/word-search/)
	- Approach : Used a helper which also keeps a visited board to know if a given element in board has already been visited. This is made true, when on char, and made false in back-tracking region after all subsequent recursion calls. This helper is called from all indices as starting point.


[https://leetcode.com/problems/prefix-and-suffix-search/](https://leetcode.com/problems/prefix-and-suffix-search/)
