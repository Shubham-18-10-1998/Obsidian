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

                 Tree Traversals
                       |
          +------------+------------+
          |                         |
         DFS                       BFS
          |                         |
    +-----+-----+                 Queue
    |     |     |
 Pre   In    Post
    |     |     |
 Recursion / Stack



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
	- Approach : 
		- DFS Approach : Maintain a class variable for maxDepth, and a class variable for the List for result. Then we recursively visit the tree using root -> root.right -> root.left. In the auxiliary function we also supply depth as depth + 1 where depth is depth of root and hence for child it will be depth+1. Then as we need only one for each level, we compare depth with maxDepth and if its greater we update the maxDepth and then add value to result because our auxiliary function to visit nodes from right to left, hence the first occurrence for a new depth will be the right most occurrence for that level. An optimisation is instead of maxDepth we can use the list size as our depth signal.
		- BFS Approach : Use the level order traversal for the tree where level size is maintained in the q, and in the q when the levelSize variable = 1, then this is the last node at that level, and hence its added to the result list. 
	- Status : Solved
- [Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/)
	-  Approach : Get left depth + right depth for each node as that value maxed is the diameter of the tree.
		- Learnings :
			- If we add 1 to each left and right depth, then we add additional to each step. While returning depth we return max(left, right) + 1 which manages depth and we use that.
			- Also to optimise use a class instance variable, so the recursion returns the height, but while doing so, we also update the class instance variable if we encounter a higher diameter. That way each node is visited only once.
	- Status : Solved
- [Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/)
	- Approach : For each node compute the left depth and right depth. Check if the tree is balanced. If not set flag to false, and stop computing height after that by returning zero subsequently.
	- Learnings
		- Balanced Tree : the sub-trees don't differ in depth by more than 1.
		- Depth returned is max(left, right) + 1
	- Optimal Approach : return -1 if we encounter unbalanced tree, or else propagate height. and then while returning check if either value is -1. then we return -1 itself.
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
		- Also for Level by level result we need to maintain q size at each level, but for BFS, we don't need to do that.
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
- [Iterative Preorder Traversal](https://www.geeksforgeeks.org/problems/preorder-traversal-iterative/1)
	- Concepts : #Stack #BinaryTree #BinaryTreeTraversal
	- Solution : Here since we have to do it iteratively, we use an explicit stack so we can perform the traversal. One important cavaet is while inserting into the stack, we insert the right child first and then the left, so that in the pop, we get the left child first to process based on the LIFO principle of stack.
	- Learnings:
		- ArrayDeque doesn't allow the insertion of null elements.
	- Status : Solved
- [Iterative Inorder Traversal](https://www.geeksforgeeks.org/problems/inorder-traversal-iterative/1)
	- Concepts: #Stack #BinaryTree #BinaryTreeTraversal 
	- Solution: Here we have to exp0lore the left tree as far as its child is not null. Once we find out its null, that means the node is ready to be processed. Then we check if node.right != null. if it isnt, we add it to stack and continue the above process. Or else while tis null. this sub-tree is processed and the parent is ready to be processed.
	- ![[Diagram.png]]
- [Path Sum](https://leetcode.com/problems/path-sum/)
	- Concepts : #Recursion 
	- Solution : For every node, we let recursion handle the problem for us. We establish our base conditions as 
		- If root == null, return false because we are already checking leaf node condition as well
		- If root.val == targetSum, and its a leaf node then true
		- Else return func(root.left, target - root.val) || func(root.right, target - root.val)
	- Learnings
		- A leaf node has no children
	- Status : Solved
- [Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)
	- Concepts : #Recursion #Universal-Variable
	- Solution : So the important parts to it are
		- In-order : left -> root -> right, thus we can use this to split the array to know the left sub-tree and right-sub-tree for the current root.
		- Pre-Order : root -> left -> right. Thus iterating this tells us the next available node to be made.
		- We combine the two. Since we are essentially constructing using the recursion using the pre-order traversal logic, we keep a universal preorder index pointer, and this points to the next val which would would be the node value. Simultaneously, we use the in-order to know limits for the left-subtree and right-sub-tree for the root. if start > end we know it is a null node. Hence our function iterates the pre-order while using the in-order to know the limits for the left and right child which are called recursively.
		- In short Pre-order tells us what node to use next, and inorder helps us finds the limits for the left and right sub-child and also know if the current node is the correct place for it using the limits.
	- Learnings :
		- Using two different traversal for different purposes to achieve a common goal.
	- Status : Solved
- [Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/)
	- Concepts : #DynamicProgramming #DFS #Recusion 
	- Approach :
		- I used the approach that we can use recusion to calculate the max-path-value from the child to the parent and then propogate that to each node. however when calculating this for each node, we can also see if the root + root.left_path + root.right_Path is greatest sum we encountered then we that is our result. Hence we keep a class variable that maintains the max we have encountered, and this returns the max path to the parent.
			- Now for the calculatios :
				- If left < 0 we make left = 0, as no point having a negative contribution from the child.
				- If right < 0, we make right = 0, as no point having a negative contribution from the child.
				- Then we calculate, root.val + left + right and compare with maxSum and update if its more.
				- Also for recursion, we then return max(left, right) + root.val to the parent.
	- Status : Solved
- [Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)
	- Concepts : #BinaryTree #BinaryTreeTraversal #Queue 
	- Approach :
		- Serialisation : We add children nodes to the string while processing the parent. This helps us avoid the need to add null to the queue we are maintaining for the in-order traversal. Also we don't level size or anything here cause we process nodes and add their children in.
		- De-serialisation : We maintain a q for prev level. This q is then used to add the children we are currently encountering. As the null cannot have children there is no need to add them to the q, Moreover, the string will help us add the null children as and when needed.
	- Status : Solved

