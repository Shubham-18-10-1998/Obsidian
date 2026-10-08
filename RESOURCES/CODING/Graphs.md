# Graph Theory
[[Graphs Theory]]

# Introduction
Nodes and edges are there in graphs.
They are nodes with a random assortment of connections between them.
The connections also known as edges, can be directional or bi-directional/undirected edge.

## Classification based on edges
- Directional Edges -> have a directional, eg. a-> b
- Weighted Edges -> where each edge has an associated cost/length. However these weighted edges can also be weighted.

## Cyclic and A-Cyclic graph
- If i can reach any node from any other node, then its cyclic
- If i cant do that, then its a-cyclic graph.

## Generic Structure
Node{
	int id;
	// data
}

Edge{
	Node source;
	Node destination;
	boolean isBidirectional;
	int weight;
}

Now graph is combination of nodes and edges.
Hence we use adjacency matrix or adjacency list.


## Adjacency Matrix
In Matrix 
		A       B         C          D
A             

B

C

D

Here, 0 where no edge and then we can populate the appropriate index in this matrix with edge info at it. 
eg. weight. and directional.

Problem here is that if the graph is sparsely connected, then a lot of space is being wasted with 0.


## Adjacency List
- TC -> O(N+E)
	- Here handles the number of connection, hence N x number of nodes each is connected. However we can see it as consecutive operation which are independent, then N+E.
- S.C -> O(N+E)

## Traversal of Graphs
- ### Depth First Search (DFS)
	- Start with a node and discover all it can reach, and then explore everything from that source till the final destination.
	- Goal isn't to traverse all the nodes, if you start from this node, what all nodes can i visit.
	- Sample Code : 
		- [DFS](https://www.geeksforgeeks.org/problems/depth-first-traversal-for-a-graph/1)
- ### Breadth First Search (BFS)
	- Here we don't need the condition of level order traversal as only queue is needed to see if visited or not.
	- Sample Code:
		- [BFS](https://www.geeksforgeeks.org/problems/bfs-traversal-of-graph/1)

# Problems
- [Number of Islands](https://leetcode.com/problems/number-of-islands/)
	- Concepts : #BFS #DFS #Matrix #Arrays #Union-Find 
	- Approach : Use BFS or DFS to search for 1 where instead of adjacency list we use neighbours in matrix to add them. 
	- Learnings : 
		- You have to use all neighbours(up, down, right, left), because my condition for updating island is when i find isolated ones. 
		- i is the y coordinate and j is the x coordinate in a i-j iterating loop. 
		- Make sure the conditions for addingNeighbours use >= 0
		- The way to instantiate a 2-D array is : int[][] name = {{1, 2, 3, ..}, {1, 2,..}, { 2, 3, ..}, .. {1, 2 , ..}}
		- The way to instantiate an array we are returning is return new int[]{1, 5, ..}
	- Status : Solved
- [Max Area of Island](https://leetcode.com/problems/max-area-of-island/)
	- Approach : Use BFS or DFS to search for 1 and then explore nearby islands. In this isolated graphs are 1 island and adding instead of adjacency list, use neighbours. For each island use area of it, and compare with curMax. Make the addNeighbours return the addedArea to keep track of the island area when adding graph vertex.
	- Learnings :
		- You have to add all neighbours(up, down, left, right), because thats we are updating island island.
		- i is y coordinate, and j is the x coordinate.
		- Make sure the conditions for addingNeighbours use >=0.
	- Status : Solved
- [Rotting Oranges](https://leetcode.com/problems/rotting-oranges/)
	- Approach : Use a sort of topological sort where each 2 influences its neighbours and makes them 2, and at each time while using a q for level order traversal in BFS, use a q.length before strting popping to keep track of time as only immediate nighbours becomes two at a given second of operation.
	- Learnings:
		- A mix of topological sort and BFS level order traversal.
		- The method works because even if we make multiple entries on the same level only the time matters and that cannot be affected by this. Also populating same thing at multiple levels is not possible because once 2 changed, we don't add it agin to queue. 
	- Status : Solved
- [Flood Fill](https://leetcode.com/problems/flood-fill/)
	- Approach : Use the sr, sc as original src and traverse with BFS and change color if its the same as the original color of sr,sc index
	- Optimisations :
		- We don't need a visited[][] here because we can use the originalColor as the mark of unvisited and when we go the the point we can update the color and that makes it as visited.
	- Status : Solved
- [01 Matrix](https://leetcode.com/problems/01-matrix/)
	- Approach : Used recursvie BFS in the sense at every 1 that i get, add only its neighbours, and if it is a 1, and if its unvisited, then i apply bfs, or else, i uses it value and then try computing the min for current value. 
		- Learnings : This approach is wrong, cause the way i am avoiding it as not calculated is using a very large value, but if this when calculated would provide a smaller value which the current node should use, then i am missing on that. Also if i use the vis[] = true after its value is assigned, i will be in a infinite loop between two adjacent 1s.
	- Optimal Approach : Use BFS with 0 as the source and let them reach 1s. This was when we reach a once, its the quickest way possible from 0. this prevents the problem we were facing about 1s getting reached in minimum time from 0.
	- Status : Solved.
- [Clone Graph](https://leetcode.com/problems/clone-graph/)
	- Approach : We use a map to keep track of nodes with index as key so that if the node has already been encountered in the adjacency list, then we can use the same node for other occurrences too. Other than that we use a set of integers with index being stored to keep track if the node with that index has been visited. Then we deep clone the first one, put it in the map, don't put it into the set as its neighbors list hasn't been updated. We use BFS logic of queue to get node, if its visited, then we skip, or else we work on the node to create nodes or fetch existing ones to add to list and update it.
	- Learnings : 
		- Cant assign ArrayList<> to List, as parent cant hold reference of child.
		- You need to read from old and write into new ones. my approach is a sort of hybrid.
		- computeIfAbsent already returns a value, so we only need to add the value in case of absent and that value is the returned
			- map.computeIfAbsent(key, n -> newValue for key)
		- In optimal solution, we have to add clone only first time encountered, not when visited.
	- Status : Solved
- [Accounts Merge](https://leetcode.com/problems/accounts-merge/)
	- Concepts : #Graphs #BFS #Maps #Sets #Sorting #Collections 
	- Approach : Initially tried using a hash-map to make groups, and then checked if there were any matches. But this approach doesn't work cause we also need to account for transitive merges, ie. a->b and b->c then we link a->c also in some way. Hence we need to use graphs. We choose one email to be primary, Now each node is connected to primary and primary to each node. (they are present in each others children). This was when we add their edges we can traverse the connected components completely. Then this was we merge, accounts, if no match we make first email primary and then add others to it and vice versa (for child add primary). If match is there, first match is made primary. We also maintain, hash-set to see if this email already exists, and a map to fetch node for each email. Once this is done, we then go to each map entry in name, List of node, and then we get the account, sort it and then give result.
	- Learnings :
		- Because of these transitive connections, we needed graphs.
		- Each node also has a visited in it, which helps us during BFS.
	- Status : Solved
- [Multi Source Flood Fill](https://leetcode.com/problems/multi-source-flood-fill/)
	- Concepts : #BFS #Graphs 
	- Approach : We use BFS to add neighbours for each colour. Initially to q all sources are added, and we keep timer at 0, now we do BFS using level traversal. This way we can keep track of timer for each point to see if its same time or not. Then when popping from the queue, we pop the point, first check if timer<=time for that given point, if yes, then we check if its unchecked point or ifs color is less that current point, then we give it the current color, or else skip. We use a addDirection function to add directions for each point.
	- Learnings:
		- For improvement, we add the colours with node, and also their time for neighbours. But before processing and adding neighbours, we check if its the correct color. This way we gurantee only the right color neighbours propogate.
		- Suggestion was to add from time of parent, this way its fine we don't need the level order traversal of BFS. This reduces the need for us to maintain the time on the level. The base idea is the same, update the queues when encountered, so that later on you can prevent using the wrong colour states.
	- Status : Solved
- [Iterative DFS for graphs](https://www.geeksforgeeks.org/problems/depth-first-traversal-for-a-graph/1)
	- Concepts : #Stack #RecursionSimulation 
	- Approach : We add the current node and to the top of the stack if its un-visited, and then the loop checks for un-visited nodes they are marked visited and printed, and then we check its neighbours. However if its already visited, we only need to check its neighbours, and then we continue the process. However if all neighbours are iterated over and there are no un-visited nodes, then we are safe to pop it.
	- Learnings :
		- The for loop which checks the neighbours, where initially i was putting the continue wont work cause its supposed to continue for the while loop. hence we should first break from it, and then use the flag to see if we are continuing,
	- Status : Solved
- [Number of Provinces](https://leetcode.com/problems/number-of-provinces/)
	- Concepts : #Stack #DFS #Graphs 
	- Approach : We iterate through the all starting points namely 0->V-1 where V is the number of nodes. We then do a DFS to find all the connected sections and thus constitute a province. Once thats done, the outer loop when it finds a not visited and hence disconnected node from the currently visited connected components, we have encountered the starting point of the new a new province and hence result is incremented.
	- Learnings :
		- When pushing onto the stack, we can mark the node as visited, as then when tis encountered again by another node, we don't add it to the stack again.
	- Status : Solved
- [Redundant Connection](https://leetcode.com/problems/redundant-connection/)
	- Concepts : #Graphs #DFS #BFS 
	- Approach :
		- Graph Solution : So for this problem we create a graph by maintaining an adjacency list. Before each edge is added, we first do a DFS from the node1 and try seeing if node2 is reachable, cause then adding an edge from node1 -> node2 creates a cycle. 
			- Complexity : O(E*(V+E))
		- Union Find My Implementation : So you maintain a parent int[] which holds the root parent of current node. Thus the find(node) becomes essentially parent[node]. For the union(node1, node2), we iterate through the parent array and update the value of all nodes having parent[node] == parent[node2] to be parent[node1]. This was the root of the now connected components is maintained. and thus when an edge is encountered where parent[node1] == parent[node2], since they are already connected this node creates a cycle and hence we can return this edge.
			- Complexity : O(N^2)
			- Leanings : In the union function when iterating also have the condition i != node2 cause during the iteration we dont want to change the parent[node2] as then other children not encountered yet will not be updated. and hence after the loop, the parent[node2] is updated to be parent[node1]
		- Find with Path compression and Union : Here we use a find(x) function which finds the root till the condition where parent[cur] != cur. However in the process i also add these nodes to a list and later for all update their parent to the root. Union now just updates the parent[parent[node2]] = parent[parent[node1]]. because the find thats called before already does path compression and thus now for the nodes1, and node2, their parents are the root.
	- Learnings :
		- Initially tried using the logic that if both nodes in an edge are already visited, then it must be the node causing the cycle to be formed, but thats not the case cause the two edges might be parts of two dis-connected parts of the graph and now are providing a join between the two. Hence wrong
	- Status : Solved.
- [Pacific Atlantic Water Flow](https://leetcode.com/problems/pacific-atlantic-water-flow/)
	- Concepts : #ReverseTraversal #BFS #Graphs 
	- Approach : So the important detail here is to understand its better to do the reverse approach of seeing if that ocean can reach a point. This way we need to add it only once, to the queue, Whereas if we were doing it the other way round, we woudn't know if i reach a point is that point already reached by ocean and the way to mark a point reached would be harder. Also i would then have to do traversal for each point again and again to see if it reached the ocean which this avoids.
	- Learnings :
		- The most crucial part is understanding that reversing the way of doing things greatly simplifies things
- [Graph Valid Tree](https://leetcode.com/problems/graph-valid-tree/)
	- Concepts : #Union-Find 
	- Approach : For a tree we have two conditions : 
		- There shouldn't be disjoint graphs.
		- There should be no cycles.
		- Thus we use the union-find to keep track of parents for each node, and ultimately we also iterate through the nodes to see if they all have a common parent to ensure there are no disjoint graphs.
	- Status : Solved.
- [Surrounded Regions](https://leetcode.com/problems/surrounded-regions/)
	- Concepts : #BFS 
	- Approach : We traverse from the edges from any 'O' and mark all the connected nodes as visited. Then later we traverse the board again, and if we find any un-visited 'O' we flip them all as these don't connect to the edges which is the condition to ensure not surrounded. 
	- Learnings :
		- In BFS, always mark the nodes as visited when pushing into the q.
	- Status : Solved.
- [Reconstruct Itinerary](https://leetcode.com/problems/reconstruct-itinerary/)
	- Concepts : #DFS #HierholzerAlgorithm #Graphs 
	- Approach : So initially you create anode class that has an index to iterate through the destinations from current node. This makes them get used only once.  Also we then sort the destinations for each node to get them lexicographically sorted. Then we do a DFS on the graph using a stack and append the node only when its index is equal to its destinations.size cause in post order this means it children have been explored and the parent can be explored. Thus we get our answer in the reverse order and we have to reverse this array to get the correct answer.
	- Status : Partially Solved


# Topological Sort
- Need a directed graph, because otherwise we cant say which should come before the other.
- Can view tasks as dependency which need something before the next is done. 
- NOTE : When there is a cycle, we cant make a sequence cause that dependency will not be able to be put a sequence. 
- Initial Approach : Iterate through Adjacency list and see how many places its present for others, so thats its min index. Now all nodes grouped under same index, you see if there is order within them, and then add them in that order.

## In-degree
- Number of nodes that it has dependence on. Can also be understood as what all has to be done before this can be done (task).

## Problems 
- [Course Schedule](https://leetcode.com/problems/course-schedule/)
	- Approach : Use a inDegree array for in each course which tells how many courses its dependent on. Also create an array of adjacency list for each course which tells what courses are dependent on this course. Now maintain a q which takes in courses with in-degree 0. when an element is polled from the queue, reduce indegree of all elements in adjacency list, and if its 0, add it too the queue. This loop runs till q is not empty. If in the end the length of ans array is equal to numCourse, then answer is true or else its false.
	- Learnings :
		- Can be solved by maintaining adjacency list, or by taking reverse which dependent on this depends on which all. If we go with second approach, its more complicated as we have to fetch particular ones and reduce their inDegree.
		- Use int[] for inDegree map as we have integer keys ranging from 0 to numCourses-1.
		- Also can use count to keep track of courseTaken instead of list where courseTaken is added.
	- Status : Solved 
- [Course Schedule II](https://leetcode.com/problems/course-schedule-ii/)
	- Concepts : #Graphs #TopologicalSort
	- Approach : We use a similar approach to course schedule where we maintain an inDegree array to see what courses have indegree == 0 and then accordingly add them to the queue. We also maintain a graph using array of List of integer where for each element, tis list contains all its dependent courses cause then we can reduce their inDegree and then add them to the queue. Only change is while popping from q, we also add them to result[] array using result[index++] and then use index == numCourses to see if all were processed, or else we return an empty array;
	- Status : Solved.

# Bipartite graph

So for this the conditions are : 
- A graph is **bipartite** if the nodes can be partitioned into two independent sets `A` and `B` such that **every**edge in the graph connects a node in set `A` and a node in set `B`. Thus there can be no edge to connect nodes in the same set.

## Problems
-  [Is Graph Bipartite?](https://leetcode.com/problems/is-graph-bipartite/)
	- Concepts : #BFS #Sets 
	- Approach : We initialise the color[] array to have all zeros by default. then while iterating for all nodes, if a node is unvisited then we first iterate its neighbours and the first one we find which is visited, we use its color to mark the node the opp color. If none are visited, then its default color = 0 stays. Then we use a BFS for the nodes, and then check if their neighbours are visited then we see. if it has the same color as the current calling node and then we return false, else if its unvisited then we color it and it to the q.
	- Status : Solved.

# Dijkstra Algorithm
Should be +ve weighted graph
Helps calculate the shortest path from one to any other node.
Once process (Popped dis with given node), thats the min distance to the node.

## Problems
- [Network Delay Time](https://leetcode.com/problems/network-delay-time/)
	- Approach : Implementation of Dijkstra's Algorithm to find min time to reach all nodes. Then for the questions the  max-time is the answer. If anything is not reachable and hence time is infinity, then return -1.
	- Learnings : 
		- Create an adjacency list to make the code faster instead of rechecking the time times array again and again where many not used modes are also being iterated through.
		- When offering to the pq, update the dist[next] also so we can compare in the future and if its lesser, then we discard by not using it to compute other nodes cost after passing through this node.
	- Status : Solved


# Min-Spanning Tree
Convert graph to tree with min length of edges
Prim’s  → grows MST from a starting node (node-centric) : the code I wrote
Kruskal → builds MST by sorting edges (edge-centric)

## Problems
- [Minimum Spanning Tree](https://www.geeksforgeeks.org/problems/minimum-spanning-tree/1)
	- Approach : Create an adjacency list, a priority queue for getting the edges with least cost to add again, and also a visited array. The keep popping the nodes with based on wt which is least and use only if node is un-visited.
	- Learnings :
		- This is Prim's Algorithm.
		- Since you have an undirected graph, you also have to add the opposite edges to your adj list, as then helps keep track of direct connection which otherwise would have been missed
		- In the declaration, List<int[]>[] adj = new ArrayList[V], we have to add @SuppressWarnings("unchecked") as other wise it breaks compilation
		- TODO : Kruskal's Algorithm.
	- Status : Solved


# Problems
https://leetcode.com/problems/course-schedule-ii/description/ (BOTH 1 & 2)


https://leetcode.com/problems/cheapest-flights-within-k-stops/description/

https://leetcode.com/problems/min-cost-to-connect-all-points/description/?envType=problem-list-v2&envId=minimum-spanning-tree

# Learnings
- Can pass non-primitive to child in recursion, and they do get updated by child operations as everything is passed by reference.