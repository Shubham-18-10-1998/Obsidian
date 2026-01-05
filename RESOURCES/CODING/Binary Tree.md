# Introduction
- Like a linked list
- Different in the sense that each node points to at most two children.
	- Done by pointers to left and right child
	- Here root is like the head of a inked list

## Traversals
Three types
- Pre-Order
	- Node, Left, Right
- In-Order
	- Left, Node, Right
- Post-Order
	- Left, Right, Node


## Sub-Tree
A tree which has a child node as a root. So hence structure of tree becomes node with left subtree and right sub-tree

# Problems
- [Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)
	- Approach : We have to do leftNode, Node, RightNode. So we assume we get left answer from left call. Append Node to list. And then get list for right Node and then Append that to existing result to return. But first before processing check if node is null, then we return.
	- Status : Solved
- [Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/)
	- Approach : We have to do node, left, right.
	- Status : Solved
- [Binary Tree Postorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal/)
	- Approach : We have to left, right, node.
	- Status : Solved
- [Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
	- Approach : We have to get depth where null root = 0 depth. then for each sub-tree, we use max(left, right) and return this result + 1.
	- Status : Solved
- [Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/)
	- Approach : Get the depth of the tree as for each level we will have one answer. Then maintain a visited of size depth, and also res of size depth. Then we recursively visit right, node left, that way the rightmost at depth is visited first and then we can mark it as visited.
	- Status : Solved
	- Comments : 
		- TODO : Learn about level order traversal for tree as it simplifies the solution.
- [Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/)
	-  Approach : Get left depth + right depth for each node as that value maxed is the diameter of the tree.
	- Status : Solved
- [Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/)
	- Approach : For each node compute the left depth and right depth. Check if the tree is balanced. If not set flag to false, and stop computing height after that by returning zero subsequently.
	- Learnings
		- Balanced Tree : the sub-trees don't differ in depth by more than 1.
	- Status : Solved
- [Top View of Binary Tree | Practice | GeeksforGeeks](https://www.geeksforgeeks.org/problems/top-view-of-binary-tree/1)
	- Initial Approach : Do a level traversal for Binary Tree. And add values for the first index and last index of the queue for a level
	- Why It is wrong : 
		- The node can be the left child of a right child which will not be visible from the top
		- The we tried adding the flag of the parent being right or left to child to see, but this doesn't work cause a right node child can branch left enough to be seen from the top.
	- Final Approach : Added a displacement for each node which is parent displacement  - 1 for left child and parent Displacement + 1 for right child. This way, we get only edge children at the level
		- NOTE : We should only use displacement to add to result array front or back because the first node might be a null in level and the second might be the leftMost one at that level.
	- Status : Solved
- [Bottom View of Binary Tree | Practice | GeeksforGeeks](https://www.geeksforgeeks.org/problems/bottom-view-of-binary-tree/1)
	- Approach : Do level Order traversal for the tree. Main parallel queues, one for nodes and another for the displacements. Also maintain a map for keeping track of the latest value found for a given displacement. As we need bottom view, as we traverse, the new values are what should make the answer and hence over-write the older ones.
	- Status : Solved
- [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)
	- Approach : Add the nodes for a particular level in the queue. These are all the children for nodes in the previous level. then we take levelSize by seeing current q.size(). Iterate through these many elements from queue and while doing so keep adding their children to the queue which make up the subsequent level. Do this till q is not empty. For each level keep a new array to add elements to, and then add this level array to the result.
	- Status : Solved
- [Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/)
	- Approach : We use the diameter for binary tree approach to find the the max path. We use an auxiliary helper function to calculate max left path and max Right path. If any are negative, we make them zero as then we wont include them in the path.  Then at each node we compute the maxPath that passes through it and compare with class instance variable to see if its larger and then make that the result if it is larger.
	- Status : Solved

