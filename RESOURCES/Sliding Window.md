# Introduction
The need arises by reducing the repetitive work. For eg. - In max sum in sub-array of size k, if the problem is handled by Brute Force, we can run two loops, i goes from 0 to n and j goes from i to i+k, however when we are adding these numbers up, between two consecutive iterations, the addition of k-1 numbers is being repeated. These is solved by using the sliding window approach.

# Identification 
- Will be a question for an array or string
- The requirement will be a continuous subsection of the whole, ie. sub-array / sub-string.
- Largest / Maximum / Smallest / Minimum will be asked.
- Window Size : 
	- Fixed Size Window - We are given the window size, and then find max/min value accordingly.
	- Variable Window Size - Here we are given a condition for which we have to find the largest or smallest window size. eg. Find the size of largest/smallest window in sub-array with sum 5. 

# Problems
## Fixed Size Window :
- [Max Sum Subarray of size K](https://www.geeksforgeeks.org/problems/max-sum-subarray-of-size-k5313/1)
- [First negative in every window of size k](https://www.geeksforgeeks.org/problems/first-negative-integer-in-every-window-of-size-k3345/1) : 
	- Learning : Check if the queue is empty or else it can behave in unexpected manner causing the code to crash.
- [Count Occurences of Anagrams](https://www.geeksforgeeks.org/problems/count-occurences-of-anagrams5839/1)
	- Learning : Using a count for the size of map to not have to iterate the whole map to keep track of how many characters are satisfied in the anagram condition. This reduces the whole complexity of having to reiterate the map.
- [K Sized Subarray Maximum](https://www.geeksforgeeks.org/problems/maximum-of-all-subarrays-of-size-k3101/1#naive-approach-using-nested-loops-on-k-time-and-o1-space)
	- Learning: 
		- 1.) Achieved Success using a priority queue type structure using map<int , vector<int>> . This allows insertion, deletion, finding in O(log(n)) complexity. Which made overall complexity O(n*log(n)).  Ideal way is to use priority queue which maintains max heap. Min heap is a special case which can also be implemented.
		-  2.) Optimal Solution is to use Deque which allows insertion and deletion at both ends of the Queue in constant (O(1)) time. The basis for the solution is that if an element is greater than elements preceding it, then it will be the greatest element in any window which comprises of it and the previous numbers. Hence in deque you elimate (pop_back) all elements while inserting in the queue which are smaller than the element encountered in the current iteration (arr[j]). While shifting the window, the only consideration is if the dq.front() == arr[i]. Now also duplicate same elements will be filled in the dequeue based when they are encountered and hence there is no problem eliminating the front in this way as if there were multiple, then even in the queue there will be multiple.
- []()
