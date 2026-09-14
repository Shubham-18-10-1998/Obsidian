
# Binary Search Tree
## Introduction
For every node : 
Left subtree - All values smaller than node value
Right Subtree - All values larger than the node value

In-order traversal is sorted sequence of values in the tree

Worst case Time Scenario - O(N)
Average case Time Scenario - O(log(N))

Balanced:

        8
      /   \
     3     10
    / \      \
   ...       ...

height ≈ log n
        ↓
search ≈ O(log n)


Skewed:

8
 \
  10
    \
     14
       \
        20
          \
           ...

height ≈ n
        ↓
search ≈ O(n)

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
			- Bottom-Up Approach : For the range approach, each child returns to its parents its min, max int[] array. Then the parent uses it to validate if its a BST, as root > left.max and root < right.min. This should always be true. If not then its not a BST. if it is true, then we update the ranges, left.min and right.max and then we send those from the parent.
			- Top-Bottom Approach : The parents supply their max and min to children nodes and they are then are validated to lie within those ranges, or else they return false which id propagated back upwards.
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
- [Delete Node in a BST](https://leetcode.com/problems/delete-node-in-a-bst/)
	- Concepts : #Recursion #BST 
	- Approach : In a Binary Search tree, if we want to delete a node, then ideal way is to replace it with the val of its smallest right sub-child. This is because its smaller than all the other right children, and greater than all left children. However there are cases that rise up:
		- If the node.right == null, then root can just become root.left;
		- If node.right != null, then let cur = node.right
			- if cur.left == null, then cur.left = node.left and return cur;
			- Else find the smallest node. and then, prev.left = smallest_node.right. We do this because for the smallest node, we know it cannot have a left child, however it not having a right child is not guaranteed. and finally root.val = smallest.val;
		- Else during recursion when finding the node, use the BST logic, 
			- root.left = deleteNode(root.left, val); (when root.val > val)
			- root.right = deleteNode(root.right, val); (when root.val < val)
	- Status : Solved
- [Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)
	- Concepts : #BinaryTreeTraversal #Recursion #Stack 
	- Approach :
		- Recursion : Use the in-order traversal to get the sorted array and from that array we can return the k-1 index element as its 1 indexed array based on the problem.
		- Iterative : We use the iterative in-order traversal to see how many nodes we have processed and when k == count of processed nodes, we return cur.val. For iterative traversal refer to : Iterative in-order traversal in Binary Tree notes.
	- Optimisations:
		- We can use a counter to know we have k values and then stop looking for an answer. This reduces the auxiliary space required.
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