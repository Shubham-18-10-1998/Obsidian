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
Here the condition is the window size, hence we maintain it constantly and try maximising or minimising something within that window.
### General Format :
![[Pasted image 20250731222239.png]]
Problems -
- [Max Sum Subarray of size K](https://www.geeksforgeeks.org/problems/max-sum-subarray-of-size-k5313/1)
- [First negative in every window of size k](https://www.geeksforgeeks.org/problems/first-negative-integer-in-every-window-of-size-k3345/1) : 
	- Learning : Check if the queue is empty or else it can behave in unexpected manner causing the code to crash.
- [Count Occurences of Anagrams](https://www.geeksforgeeks.org/problems/count-occurences-of-anagrams5839/1)
	- Learning : Using a count for the size of map to not have to iterate the whole map to keep track of how many characters are satisfied in the anagram condition. This reduces the whole complexity of having to reiterate the map.
- [K Sized Subarray Maximum](https://www.geeksforgeeks.org/problems/maximum-of-all-subarrays-of-size-k3101/1#naive-approach-using-nested-loops-on-k-time-and-o1-space)
	- Learning: 
		- 1.) Achieved Success using a priority queue type structure using map<int , vector of int > . This allows insertion, deletion, finding in O(log(n)) complexity. Which made overall complexity O(n*log(n)).  Ideal way is to use priority queue which maintains max heap. Min heap is a special case which can also be implemented.
		-  2.) Optimal Solution is to use Deque which allows insertion and deletion at both ends of the Queue in constant (O(1)) time. The basis for the solution is that if an element is greater than elements preceding it, then it will be the greatest element in any window which comprises of it and the previous numbers. Hence in deque you elimate (pop_back) all elements while inserting in the queue which are smaller than the element encountered in the current iteration (arr[j]). While shifting the window, the only consideration is if the dq.front() == arr[i]. Now also duplicate same elements will be filled in the dequeue based when they are encountered and hence there is no problem eliminating the front in this way as if there were multiple, then even in the queue there will be multiple.
-  [Longest Harmonious Subsequence](https://leetcode.com/problems/longest-harmonious-subsequence/)
	- Learning:
		- 1.) Since it requires sub-sequence and we can skip the elements in the middle to only include select elements, sorting and re-arranging doesn't break the condition of the question. This approach also allows to use the sliding window approach.
		- 2.) An alternate is using hash-map to find if the elements with difference 1 are present and then using that approach to find the solution.
- [Contains Duplicate II](https://leetcode.com/problems/contains-duplicate-ii/)
	- Learning:
		- 1.) Original Approach was to maintain a map where the key-value pair represents element, index. Now if element doesn't exist in the map, insert it or else check if current index minus the value for index is <=k. If it its true return true or else if whole loop is traversed without it becoming true, return false. Here the complexity is O(n x log(n)) as count in cpp has complexity has time complexity of O(log(n)).
		- 2.) New Approach learnt is that, we can use unordered_set which has constant time complexity for insert, delete count etc functions. This helps bring the complexity to O(n).
## Variable Size Window:
Here the condition isn't the window size, and the point is to maximise or minimise the window size itself, based on a given condition.
### General Format 
![[Pasted image 20250730085838.png]]
Problems-
- [Longest Substring with K Uniques](https://www.geeksforgeeks.org/problems/longest-k-unique-characters-substring0853/1)
	- Learning: The window size is alway moved to increase.Because there are 2 possibilities, if the one added element, which gets it over the limit, causes the one element to be eliminated, and then this is the same window size as before, so we can optimise by moving forward for a larger one. The other is many elements are removed to get k back to equal condition, and then we move on to increase anyway.
- [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters)
	- Learning: Be careful about what represents what and you are checking count of what in map! Another approach would be to compare the window size to the map size to realise about existence of duplicates!
- [Fruit Into Baskets](https://leetcode.com/problems/fruit-into-baskets/)
	- Learning: Used a different variable for count, however, we can also use j-i+1 , which is the window size to reflect the count value.
- [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)
	- Learning: Because of it being a min size window question, you have to work on reducing the window size by moving i forward to see if the condition is still getting satisfied. Also consider where i and j are at the end of iterations and how that will affect the window sizes.
