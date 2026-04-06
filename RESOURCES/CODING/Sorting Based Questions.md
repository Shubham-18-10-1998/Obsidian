
# Problems
- [K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/)
	- Approach : Use a aux List<int[]> where we store dist, index for all points, and then we sort the aux list and get the first k entires from aux to get index of original points and then return res
	- Learnings :
		- Can also solved by maintaining a min priority queue to get the smallest k points based on distance. This is done by adding all elements to pq and then polling k times.
	- Optimised Code : Use a max heap of size k, where we store the k smallest. if the current dis is smaller than pq.peek(), then poll() and add the new one, else skip it. This way we keep the k shortest distances.
		- Here we can add it at every step and then just poll if size is greater than k, this we are keeping the k smallest.
	- Status : Solved