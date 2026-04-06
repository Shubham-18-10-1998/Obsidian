
# Introduction
							
							Insertion                     Search
Unsorted Array                                        O(1)                                                   O(N)
Sorted Ray                                               O(N)                                                  O(log(N))
Stack                                                        O(1)                                                    O(N)
Heap                                                         O(log(N))                                          O(N.log(N))
Linked List                                                O(1)                                                   O(N)
Hash-Map                                                O(1)                                                    O(1)



Hash-Map : Key-Value Pairs data-structure
Searching for a key is -> O(1)

Tree-HashMap : The keys are also sorted

# Problems
- [Two Sum](https://leetcode.com/problems/two-sum/)
	- Approach : With Hash-Map we use the map to keep value and index in key value pair, Then we iterate through map if for any index where we have target-nums[i] also exists in the map, we populate the array and break the loop, else we add the key-value pair.
	- Status : Solved
- [4Sum II](https://leetcode.com/problems/4sum-ii/)
	- Initial Approach : We make a frequency map for values in last array
	- Approach : Supposed to do for two arrays sum at one time to create sum frequency map.
	- Learnings : 
		- map.getOrDefault(sum, 0)
		- Approach
	- Status : Unsolved
- [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)
	- Approach : Use prefix sum to optimise the code, and then use hash-map to maintain frequency to solve
	- Learnings : cant keep res++ for sum equal to k as it needs to know all values before it for which the sub-sum is 0.
	- Status : Unsolved
- [Ransom Note](https://leetcode.com/problems/ransom-note/)
	- Approach : Use a int[] of length 26 as map for both magazine and ransomNote to maintain char count. Once poulated for both. iterate through the two arrays and if map_ransomNote[i] > map_mag[i] then return false, cause then it cant be constructed or else return true.
	- Status : Solved
- [Valid Anagram](https://leetcode.com/problems/valid-anagram/)
	- Approach : create an int array of length 26 to function as map for string s. Put check if they are of unequal length, then return false. When iterating through t, before reducing count check if the count in map there is already 0 return false, or else reduce count and continue. if you are able to iterate through the loop, then it will be all zeroes in the end as they are of same length and no count went into negative. Hence after loop return true.
	- Status : Solved
- [Longest Palindrome](https://leetcode.com/problems/longest-palindrome/)
	- Approach : Use a map to iterate through the string and update frequency of each character. Now we are allowed at most one odd frequency (as this can come in the centre and still be palindrome) and rest all should be even hence we can add for all others freq - (freq%2).
	- Learnings :
		- map.merge(key, 1, Integer::sum) is used to increase freq of chars by one and instantiate with 1.
		- mag.values() gives iteratable for all values of map
- [Roman to Integer](https://leetcode.com/problems/roman-to-integer/)
	- Approach : Create a map<Character, int[]> for storing priority and value for each char, and then iterate from the back. If priority cur < priority prev, then value is subtracted, or else value is added.
	- Learnings : 
		- Don't need priority as the priority is same as value and that can directly be used. Hence we only need a map for <char, int>. Also we can use int[128] as ASCII values range from 0 to 127.
	- Status : Solved
- [Time Based Key-Value Store](https://leetcode.com/problems/time-based-key-value-store/)
	- Concepts : #Hash-Table #String #BinarySearch #Design 
	- Approach : Used a map of String, Deque<Pair<String, Integer>>. This was we have notion of min value using getFirst() of Deque, and max element using getLast(). Also in case its between them, then we use a descending iterator to get the value in between.
	- Learnings : 
		- For Iterator i.next() returns Object. So to resolve this, we make Iterator<Pair<String, Integer>>. And then use i.next() once to get the pair we are on now. And then use the values to compare.
	- Optimal Solution : We store the values as map<key, List<Pair<Integer, String>>. This was we can use binary search to utilise the constraint that values are strictly increasing.
	- Status : Solved

Questions : 

1. **https://leetcode.com/problems/longest-consecutive-sequence/description/**

2. https://leetcode.com/problems/top-k-frequent-elements/description/

3. https://leetcode.com/problems/two-sum/description/

4. **https://leetcode.com/problems/4sum/**

5. **https://leetcode.com/problems/contains-duplicate/description/**

6. **https://leetcode.com/problems/valid-anagram/description/**
