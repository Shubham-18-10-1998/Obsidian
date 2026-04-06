
# Introduction
**Trie is a tree where each path from root to a node represents a prefix of words, and words share their common prefixes.**
Features
- Its a smart way to store words, such that the time complexity to search it is O(L).
- It also provides storing the common prefix of words multiple times.

# Implementation
- [Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree/)
	- Concepts : #Trie #Hash-Table 
	- Approach : I create a class for TrieNode with instance variables Character c for the Character of the node. I used Character so i can store null for the Trie head node. Other than that i had a list for children nodes so i can iterate through the kids for subsequent letters.I also have a wordEnds flag to know if a word ends at this node. For search and insert, i used a helper functions. Search prefix and word have same implementation with the change that for prefix last char node need not have wordEnds = true.  For insertHelper you iterate through children to find the child, if it exists, then we continue from the new found node, else we add a node for it, and then continue with the newly added node.
	- Learnings : 
		- We need to return from iterating the list if found so that subsequent add childNode logic isnt called
		- We can also use an array[] so we have constant lookup time instead of having to iterate through the entire list;
		- Top level class cannot be private, it can only be public or default. Inner classes can be anything.
		- TrieNode class inside the Trie can be private static class TrieNode. This make it more memory efficient, doesn't make it dependent on the reference of the inner class to be initialised, and also prevents it from accessing the variables of outer class (Trie in this case).
	- Status : Solved

# Problems
⭐ **If you're learning DS deeply**, the next important Trie concepts are:

1️⃣ **Compressed Trie (Radix Tree)**  
2️⃣ **Ternary Search Trie**  
3️⃣ **Using Trie for prefix problems (Top-K autocomplete)**  
4️⃣ **Bitwise Trie (for XOR problems)** — extremely common in interviews.
