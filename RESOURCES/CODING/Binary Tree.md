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
		- Learnings :
			- If we add 1 to each left and right depth, then we add additional to each step. While returning depth we return max(left, right) + 1 which manages depth and we use that.
	- Status : Solved
- [Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/)
	- Approach : For each node compute the left depth and right depth. Check if the tree is balanced. If not set flag to false, and stop computing height after that by returning zero subsequently.
	- Learnings
		- Balanced Tree : the sub-trees don't differ in depth by more than 1.
		- Depth returned is max(left, right) + 1
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
	- Learnings : 
		- You can add a check to not add null values to the queue to prevent them from being processed by q at a given level.
	- Status : Solved
- [Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/)
	- Approach : We use the diameter for binary tree approach to find the the max path. We use an auxiliary helper function to calculate max left path and max Right path. If any are negative, we make them zero as then we wont include them in the path.  Then at each node we compute the maxPath that passes through it and compare with class instance variable to see if its larger and then make that the result if it is larger.
	- Status : Solved
- [Same Tree](https://leetcode.com/problems/same-tree/)
	- Approach : Compare the nodes, and if there is no cause of inequality there, then call same function on right of both and left of both. If either is false, return false, or return true. Conditions to check are if both together are non null and not same val then false, if both null then true, if only one null, then false, and otherwise, compare left and right for both.
	- Status : Solved
- [Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/)
	- Approach : Take left and right node of tree. Store them and invert them. Then make root.left = right and root.right = left, and then return root.
	- Status : Solved
- [Symmetric Tree](https://leetcode.com/problems/symmetric-tree/)
	- Approach : Used Level Order traversal for each level from level 1. Now we use teo dequeue, one to add left elements with offerLast and to add rightElements with offerFirst. Then we pop levelSize()/2 times and compare. if they are equal till the q doesn't become empty the symmetric, or else not symmetric.
	- Learnings : 
		- LinkedList<> is Deque implementation to allow nulls and by default is a queue but can use offerFirst offerLast, pollFirst and pollLast to make it function like double ended queue.
	- Optimised Approach : You can add them in queue in relative order of left.left right.right and left.right, right.left. this ensures we pop the mirrored bits together. which is what we need. Also since binary tree, we will always add in pairs anyway.
	- Status : Solved
- [Subtree of Another Tree](https://leetcode.com/problems/subtree-of-another-tree/)
	- Approach : Recursively see if there is match in node and subNode values. If there is then call a helper matcher function to see if there on onwards its a perfect match or else compare root.left and subRoot and root.right and subRoot to see if the subTree exists there.
	- Learnings :
		- Need helper to see if perfect match is there cause that allows only one logic flow, where as parent function also allows logic off subTree matching subRoot tree. and this isn't allowed once a match has been found cause for match of subTree, middle skips aren't allowed.
	- Optimised Approach :
		- Use KMP for string matching after converting to String for tree and subRoot
		- Using Rolling hashing where every subTree gets a hash and match them for every node with subTree to see a match
	- Status : Solved
- [Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)
	- Concepts : #Recursion #BinaryTree #Stack #Set
	- Approach : I create a map for each node to store it parent through recursive helper function. Then for one of the nodes i create a set to store all its parent. For the other i create a stack adding its parents. Since stack uses LIFO, this gives me slowly the lower and lower parents common thus making the last common value the lowest common ancestor. The while popping from the stack i see if its in set of the other node, then its a possible common ancestor. If not i break, and then previous value put for res is the answer. In the start i use base condition that is root equals either of the TreeNode , then root is the answer.
	- Optimal Solution : 
		- base idea is that when we encounter p or q,  return it, and use this as signals to know we have found them or they a null to show we have not found them. Now whenever left and right return non-null, it means that this node is LCA cause that means that left had p and right had q or vice versa OR one side has the needed LCa and that gets propagated upwards. The returning also reduces further costs ie. in case the other node is a child of this node found first, then the LCA is the node found first.
	- Status : Solved

