# Introduction:
Essentially if we are trying to find a string s1  with length l1 in another string s2 with length l2, then one way, that is the brute force approach is to at every index s2, we start a loop of length l2 to see if we find s1, or else we increment he pointer by 1 and then repeat the process. This leads to the worst case complexity of O(l1 x l2), which in essentially O(n^2) complexity. Hence to optimise this, we use certain algorithms as below.

# KMP Algorithm
## Basic chronology -
1. Create LPS array (Longest Prefix Suffix array). Note this is made for the pattern string.
2. Then comparison is done with the longer string in which we have to find occurrence.

## Longest Prefix Sufix Array (LPS)
It is created to have the length of the longest **common** pure prefix suffix length for the substring pat.substr(0, i) where i is the i-th element of the LPS array. 
Note: single elements have pure prefix suffix length as 0 because pure prefix suffix means that it cannot be the string itself.
Note: LPS is made only for the pattern string. 
Note: Same character cannot be part of the suffix and prefix.
eg. ABCABCA
Here for this string the LPS value is 1 and not 4 as ABCA assumes the A in the middle is part of both, which is not allowed. **But if you want to further optimise the algorithm, it's allowed!**
- eg. If pattern string is : ababd
	a -> 0
	ab -> 0 : as prefix is a, suffix b 
	aba -> 1 : as longest possible common prefix and suffix is a, hence length = 1
	abab -> 2 : here its ab
	ababd -> 0
	Hence the LPS array comes out to be {0, 0, 1, 2, 0}

## Working of the Algorithm
- In Case of match s[i] and pat[j], we increase (i++, j++) the pointers
- In case of mismatch, 
	- if j != 0, j is replaced with lps[j-1] and we continue matching.
	- if j == 0 and even then mismatch happens, then just i++

## Why does j -> lps[j-1] change happen, and how does it work?
The LPS array represents the length of the common prefix suffix. Which means the same prefix and suffix for the substr = pat.substr(o, i). Hence if the element in that index is say x, that means the first x letters of the pat substring and the last x letters are equal. Which also means if a comparison was started from j=0 for the pattern, the first x would match  as they form the suffix for lps[j-1] AND lps[j-1] is also prefix of the pattern which allows to move the j forward by x values for the pattern as they have already been matched.

![[Pasted image 20250729215901.png]]




