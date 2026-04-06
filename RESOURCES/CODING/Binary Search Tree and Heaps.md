
# Binary Search Tree
## Introduction
For every node : 
Left subtree - All values smaller than node value
Right Subtree - All values larger than the node value

In-order traversal is sorted sequence of values in the tree

Worst case Time Scenario - O(N)
Average case Time Scenario - O(log(N))

## Problems
- [Search in a Binary Search Tree](https://leetcode.com/problems/search-in-a-binary-search-tree/)
	- Concepts - #BST #Recursion 
	- Approach : Use the property of BST to determine the sub-tree to be pursued. ie, if val > root.val -> search in root.right, else if root.val > val -> search root.left. Base conditions are
		- If val == root.val -> return root
		- if root == null -> return null;
- [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)
	- Approach :
		- 1. Make in-order traversal array and then check if its strictly increasing.
		- 2. Use a range approach as left can be only lesser than its value and right has top be greater than its value
		- Used the range approach. Use a helper function
			- isValid(treeNode root node, long min, long left)
			- validate left subtree -> isValid(node.left, min, node.val)
			- validate right subtree -> isValid(node.right, root.val, max);
	- Learnings : Can also use property of BST that In-order traversal is strictly increasing
	- Status : Solved
- [Trim a Binary Search Tree](https://leetcode.com/problems/trim-a-binary-search-tree/)
	- Approach : Get a valid node for each node, that is if value is lesser than low, search right trees till you get valid value in the limit Or if val is greater than high, search left tree till you get valid node. Then validate its left and right child.
	- Status : Unsolved
- [Lowest Common Ancestor of a Binary Search Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)
	- Approach : If we have the two values then using condition for BST, if the root val is between the two values, then its the lowest common ancestor or else, they lie on the same of the tree and we can go to that side of the tree. Another base condition if root val is equal to either of the values, then its the lowest common ancestor.
	- Status : Solved
- [Convert Sorted Array to Binary Search Tree](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/)
	- Approach : Use binary search mid to decide the node for tree. Them recursively the left side mid and right side mid will be the children nodes. This recursively working on sections of the array generates the height balanced optimal BST as we are splitting in approximately equal halves which is needed for height balanced BST. 
	- Status : Solved



# Heaps
## Introduction
Priority Queue : Same as heap
How does it work?
Min - Priority Queue : 
- Min element on the top
- Node value is smaller than left and right child
- Tree is filled in sequence : This keeps hight as log(N)

Max Priority Queue :
- Max element on top
- Node value is greater than left and right child
- Tree Filled in sequence

Can only remove max or min element in their respective priority queue.

By default min priority Queue. for max we use (Collections.reverseOrder()) in constructor of PriortyQueue to get max priority Queue.

## Problems
- Inserting element 
	- Approach : Insert at next spot, then run heapify which swaps values according to condition of the priority queue. Make the maximum of the child the new root, and then run the heapify on that side. in case of maximum priority queue.
- Removing element : make last added node as parent and then run heapify downwards. 
- [Kth Smallest Element in a Sorted Matrix](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/)
	- Approach : Max heap with size k will give me kth smallest element after iterating through all elements



1. **https://leetcode.com/problems/last-stone-weight/description/**

2. **https://leetcode.com/problems/kth-largest-element-in-an-array/description/**

3. **https://leetcode.com/problems/k-closest-points-to-origin/description**/

4. https://leetcode.com/problems/find-median-from-data-stream/description/