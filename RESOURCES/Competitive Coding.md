# C++
- ## Priority Queues 
	- Used for maintaining max, or min heaps. All functions such as push(), pop() are of log(n) complexity. Pop() function eliminates the element at the top of the heap. top() function is used to see the element at the top.
	- In this data structure the bases of ordered can also be manipulated using the bool operator in comparator struct to define your own basis for arrangement.
		- Defined as priority_queue(T, vector<T>, Comp).
		- struct myComp {
		    constexpr bool operator()(
		        pair<int, int> const& a,
		        pair<int, int> const& b)
		        const noexcept
		    {
		        return a.second < b.second;
		    }
		};
- ## Deque
	- Used for maintaining queue which is accessible front from and back. Allows insertion at front and back using push_front() and push_back() in O(1) time. Function insert() is for an position.  Function pop_front() and pop_back() is for deleting elements at front and back in O(1) time. The function dq.front() and dq.back() help in accesing elements easily at front and back.

# Sliding Window
[[Sliding Window]]