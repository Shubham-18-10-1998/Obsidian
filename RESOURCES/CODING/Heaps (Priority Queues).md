# Summary 

| Operation | Binary Heap |
|---|---:|
| peek min/max | O(1) |
| insert | O(log n) |
| remove min/max | O(log n) |
| search arbitrary element | O(n) |

Complete Binary Tree
        ↓
height = O(log n)
        ↓
Heapify Up / Heapify Down
        ↓
O(log n)

Repeated insertion:
    O(n log n)

Bottom-up build-heap:
    O(n)

Why?
Most nodes are near the bottom and can only move a few levels.


# Heap & PriorityQueue — Interview Notes

## 1. What is a Heap?

A Heap is a **complete binary tree** with a special ordering property.

There are two main types:

    Min-Heap
    Max-Heap

---

# 2. Min-Heap

In a Min-Heap:

    parent <= children

Therefore:

    smallest element = root

Example:

            2
          /   \
         5     7
        / \   / \
       9   6 8  10

Array representation:

    [2, 5, 7, 9, 6, 8, 10]

Important:

> A Heap is NOT a fully sorted tree.

Only the parent-child relationship is guaranteed.

---

# 3. Max-Heap

In a Max-Heap:

    parent >= children

Therefore:

    largest element = root

Example:

            10
          /    \
         8      9
        / \    / \
       5   6  2   7

The root is always the maximum element.

---

# 4. Complete Binary Tree

A Heap is a Complete Binary Tree.

A complete binary tree fills levels:

    left → right

without gaps.

Example:

            1
          /   \
         2     3
        / \   /
       4   5 6

This is complete.

The complete-tree property allows us to efficiently represent the Heap using an array.

---

# 5. Array Representation

Example Heap:

            2
          /   \
         5     7
        / \   / \
       9   6 8  10

Array:

    [2, 5, 7, 9, 6, 8, 10]

The tree is stored level-by-level.

---

# 6. Parent and Child Indexes

For an element at index `i`:

    parent = (i - 1) / 2

    left child = 2 * i + 1

    right child = 2 * i + 2

Parent uses integer division.

Example:

    index = 3

    parent = (3 - 1) / 2
           = 1

    left child = 2 * 3 + 1
               = 7

    right child = 2 * 3 + 2
                = 8

---

# 7. Why is Heap Peek O(1)?

In a Min-Heap:

    minimum = root = array[0]

In a Max-Heap:

    maximum = root = array[0]

Therefore:

    peek() → O(1)

We don't need to search through the Heap.

---

# 8. Heap Insertion

To insert a new element:

### Step 1

Add it at the next available position.

This maintains the Complete Binary Tree property.

Example:

    [2, 5, 7, 9, 6, 8, 10]

Insert `1`:

    [2, 5, 7, 9, 6, 8, 10, 1]

### Step 2

The Heap property may now be violated.

We move the new element upward.

This is called:

    Heapify Up

or:

    Bubble Up

---

# 9. Heapify Up

Example:

    [2, 5, 7, 9, 6, 8, 10, 1]

Compare `1` with its parent `9`.

    1 < 9

Swap:

    [2, 5, 7, 1, 6, 8, 10, 9]

Compare `1` with parent `5`.

    1 < 5

Swap:

    [2, 1, 7, 5, 6, 8, 10, 9]

Compare `1` with parent `2`.

    1 < 2

Swap:

    [1, 2, 7, 5, 6, 8, 10, 9]

Heap property restored.

---

# 10. Why is Heap Insertion O(log n)?

The inserted element starts at the bottom.

It can move upward:

    leaf
      ↓
    parent
      ↓
    grandparent
      ↓
    ...
      ↓
    root

The height of a Complete Binary Tree is:

    O(log n)

Therefore:

    insert → O(log n)

---

# 11. Removing the Minimum / Maximum

For a Min-Heap:

    removeMin()

For a Max-Heap:

    removeMax()

The root is removed.

Example:

    [2, 5, 3, 9, 6, 8, 10]

Remove `2`.

We cannot simply leave an empty root.

Instead:

    Move the LAST element to the root.

So:

    [10, 5, 3, 9, 6, 8]

This preserves the Complete Binary Tree structure.

However, the Heap property is now broken.

---

# 12. Heapify Down

After moving the last element to the root, move it downward until the Heap property is restored.

For a Min-Heap:

    Compare both children.
    Choose the SMALLER child.
    Swap if child < parent.

For a Max-Heap:

    Compare both children.
    Choose the LARGER child.
    Swap if child > parent.

---

# 13. Example of Heapify Down

Starting:

    [10, 5, 3, 9, 6, 8]

Compare `10` with children:

    5 and 3

Choose smaller child:

    3

Swap:

    [3, 5, 10, 9, 6, 8]

Now compare `10` with its child:

    8

Swap:

    [3, 5, 8, 9, 6, 10]

Heap property restored.

---

# 14. Why is Remove-Min / Remove-Max O(log n)?

The element moved to the root can travel down to the bottom.

The height of the Heap is:

    O(log n)

Therefore:

    removeMin() → O(log n)
    removeMax() → O(log n)

---

# 15. Heap Complexity

For a standard binary Heap:

    peek min/max       → O(1)

    insert             → O(log n)

    remove min/max     → O(log n)

    search arbitrary   → O(n)

Important:

> A Heap is NOT a general-purpose fast search structure.

It only guarantees fast access to the minimum or maximum.

---

# 16. Why Search is O(n)

A Heap does NOT fully sort its elements.

Example:

            2
          /   \
         5     7
        / \   / \
       9   6 8  10

We know:

    2 is minimum

But we cannot determine the location of an arbitrary value without potentially checking many nodes.

Therefore:

    search → O(n)

---

# 17. PriorityQueue in Java

Java's:

    PriorityQueue<T>

is implemented using a Heap.

By default:

    PriorityQueue = Min-Heap

Example:

    PriorityQueue<Integer> pq = new PriorityQueue<>();

    pq.add(5);
    pq.add(2);
    pq.add(8);
    pq.add(1);

    pq.peek() → 1

    pq.poll() → 1

---

# 18. Max-Heap using PriorityQueue

Java's default PriorityQueue is a Min-Heap.

For a Max-Heap:

    PriorityQueue<Integer> pq =
        new PriorityQueue<>(Collections.reverseOrder());

Then:

    pq.add(5);
    pq.add(2);
    pq.add(8);
    pq.add(1);

    pq.peek() → 8

---

# 19. PriorityQueue Complexity

    add() / offer() → O(log n)

    poll()          → O(log n)

    peek()          → O(1)

Why?

### peek()

Just access the root.

    O(1)

### add()

Insert at the bottom and Heapify Up.

    O(log n)

### poll()

Remove root, move last element to root, then Heapify Down.

    O(log n)

---

# 20. Heap vs Sorted Array

Suppose we repeatedly need the minimum element.

### Sorted Array

Sorting initially:

    O(n log n)

But maintaining sorted order after new insertions can be expensive.

### Heap

    peek minimum → O(1)
    insert       → O(log n)
    remove min   → O(log n)

A Heap is useful when the collection changes dynamically and we repeatedly need the minimum/maximum.

---

# 21. When Should I Think of a Heap?

Think of a Heap when the problem says things like:

    "Repeatedly get the smallest..."

    "Repeatedly get the largest..."

    "Kth largest..."

    "Kth smallest..."

    "Top K..."

    "Priority..."

    "Process the next highest/lowest priority..."

    "Merge multiple sorted sequences..."

The key question is:

> Do I repeatedly need access to the minimum or maximum while the data is changing?

If yes, consider a Heap / PriorityQueue.

---

# 22. Data Structure Decision

Ask:

    What operation needs to be fast?

### Need membership?

    HashSet

    contains → O(1) average

### Need key → value?

    HashMap

    get → O(1) average

### Need random index access?

    ArrayList

    get → O(1)

### Need LIFO?

    Stack / Deque

    push/pop → O(1)

### Need FIFO?

    Queue / ArrayDeque

    offer/poll → O(1) amortized

### Need min/max repeatedly?

    PriorityQueue / Heap

    peek → O(1)
    add/poll → O(log n)

---

# 23. Important Heap Mental Model

    Heap
      ↓
    Complete Binary Tree
      ↓
    Usually represented as Array
      ↓
    Root contains min/max
      ↓
    Heapify Up after insertion
      ↓
    Heapify Down after removal

Complexities:

    peek → O(1)

    insert → O(log n)

    remove min/max → O(log n)

---

# 24. Min-Heap vs Max-Heap

| Property | Min-Heap | Max-Heap |
|---|---|---|
| Root | Minimum | Maximum |
| Parent relation | Parent <= children | Parent >= children |
| peek | Minimum | Maximum |
| Insert | O(log n) | O(log n) |
| Remove root | O(log n) | O(log n) |

---

# 25. Interview Answers

### What is a Heap?

> A Heap is a Complete Binary Tree that maintains a parent-child ordering property. In a Min-Heap the parent is smaller than or equal to its children, while in a Max-Heap the parent is greater than or equal to its children.

### Why is peek O(1)?

> The minimum or maximum is always stored at the root, which is index 0 in the array representation.

### Why is insertion O(log n)?

> The new element is added at the bottom to maintain the complete-tree property and may move up at most the height of the tree, which is O(log n).

### Why is removal O(log n)?

> We replace the root with the last element to preserve the complete-tree structure, then heapify down. The element can move at most the height of the tree.

### Why isn't a Heap sorted?

> A Heap only guarantees the parent-child ordering. It does not guarantee that siblings or elements at different branches are sorted relative to each other.

### Why use PriorityQueue?

> When I repeatedly need the minimum or maximum element while the collection is dynamically changing. It provides O(1) access to the root and O(log n) insertion and removal.

---

# 26. Key Takeaways

1. Heap = Complete Binary Tree + ordering property.

2. Min-Heap → minimum at root.

3. Max-Heap → maximum at root.

4. Heap is NOT fully sorted.

5. Heap is usually represented using an array.

6. Parent/child indexes:

       parent = (i - 1) / 2
       left   = 2i + 1
       right  = 2i + 2

7. Insertion → Heapify Up → O(log n).

8. Removal of root → Heapify Down → O(log n).

9. Peek → O(1).

10. Arbitrary search → O(n).

11. Java PriorityQueue uses a Heap.

12. Default PriorityQueue → Min-Heap.

13. PriorityQueue with reverseOrder() → Max-Heap.

14. Think Heap when you need repeated min/max access.

15. The reason for O(log n) is the height of the Complete Binary Tree.

# Heap Construction — Build Heap

## 1. Two Ways to Build a Heap

There are two different approaches:

### Approach 1: Insert elements one by one

Start with an empty Heap:

    add(element)
    add(element)
    add(element)
    ...

Each new element:

    1. Goes to the next available position.
    2. May need to Heapify Up.

A single insertion can cost:

    O(log n)

Doing this for `n` elements:

    O(n log n)

Therefore:

    Build Heap using repeated insertions → O(n log n)

---

## 2. Approach 2: Bottom-Up Build Heap

If we already have an array:

    [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]

we don't need to insert each element individually.

Instead:

    1. Treat the array as a Complete Binary Tree.
    2. Start from the last non-leaf node.
    3. Heapify Down.
    4. Continue moving toward the root.

This is called:

    Bottom-Up Heap Construction

or:

    Build Heap / Heapify

Complexity:

    O(n)

---

# 3. Why is Bottom-Up Build Heap O(n)?

This is initially counterintuitive because:

    Heapify Down can take O(log n)

However, NOT every node takes O(log n) work.

The amount of work depends on how far the node is from the bottom.

---

## 4. Most Nodes Are Near the Bottom

Consider a Complete Binary Tree.

Approximately:

    n/2 nodes → leaves
    n/4 nodes → 1 level above leaves
    n/8 nodes → 2 levels above leaves
    n/16 nodes → 3 levels above leaves
    ...

The leaves have:

    0 children
    → 0 work

Nodes one level above the leaves can move at most:

    1 level

Nodes two levels above can move at most:

    2 levels

Nodes three levels above can move at most:

    3 levels

The root is the only node that can move:

    O(log n) levels

---

# 5. Rough Work Distribution

The total work looks approximately like:

    n/2 × 0
    +
    n/4 × 1
    +
    n/8 × 2
    +
    n/16 × 3
    +
    ...
    +
    1 × log n

The important intuition is:

    Many nodes → very little work
    Few nodes → more work
    Very few nodes → lots of work

The total adds up to:

    O(n)

---

# 6. Why Isn't It O(n log n)?

A common mistake is:

    n nodes
    ×
    O(log n) per node
    =
    O(n log n)

This reasoning would be appropriate if every node could require O(log n) work.

But in bottom-up heap construction:

    Most nodes cannot travel O(log n).

For example:

    Leaves:
    n/2 nodes × 0 work

    One level above:
    n/4 nodes × 1 work

    Two levels above:
    n/8 nodes × 2 work

    Root:
    1 node × log n work

Therefore the total is:

    O(n)

---

# 7. Important Comparison

## Repeated Insertion

    Start with empty Heap

    add()
    add()
    add()
    ...

Each element starts at the bottom and can Heapify Up.

    n insertions
    ×
    O(log n)

Therefore:

    O(n log n)

---

## Bottom-Up Build Heap

    Start with existing array

    Heapify Down from bottom toward root

Most nodes are near the bottom.

Therefore:

    O(n)

---

# 8. Example

For approximately `n = 16` nodes:

    8 nodes × 0 levels
    4 nodes × 1 level
    2 nodes × 2 levels
    1 node  × 3 levels

Approximate work:

    8×0 + 4×1 + 2×2 + 1×3

    = 0 + 4 + 4 + 3

    = 11

This is much closer to O(n) than O(n log n).

---

# 9. Key Interview Explanation

If asked:

    "Why is building a Heap O(n)?"

A good answer:

> Bottom-up heap construction starts from the last non-leaf nodes and heapifies downward. Most nodes are near the bottom and can only move a small number of levels, while only a small number of nodes near the root can move many levels. Therefore, the total work across all nodes is O(n).

---

# 10. Complexity Summary

| Operation | Complexity |
|---|---:|
| Insert one element | O(log n) |
| Build Heap using n insertions | O(n log n) |
| Build Heap from existing array | O(n) |
| Heapify Up | O(log n) |
| Heapify Down | O(log n) |
| Peek min/max | O(1) |
| Remove min/max | O(log n) |

---

# 11. Mental Model

Remember:

    Repeated insertion:

        Empty Heap
             ↓
        Insert one-by-one
             ↓
        Heapify Up
             ↓
        O(n log n)


    Bottom-up construction:

        Existing Array
             ↓
        Complete Binary Tree
             ↓
        Heapify Down
             ↓
        Most nodes do very little work
             ↓
        O(n)

---

# 12. Most Important Takeaway

Do NOT think:

    "Heapify is O(log n), therefore building a Heap is O(n log n)."

Instead ask:

    "How many nodes actually perform O(log n) work?"

Answer:

    Very few.

Most nodes are near the bottom and do very little work.

Therefore:

    Build Heap from an existing array → O(n)


# Problems 
- [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/)
	- Solution : We maintain a min priority queue of size k, and add elements to the pq, if they are larger then the root. This way we end up with a pq that has the k largest elements of the q, and k-th largest element is the root of this heap (pq) and can be retrieved using pq.peek().
	- Learnings : We can also achieve this using a max-heap, and then popping from it k times, but however the complexity there is O(n.log(n))  as it becomes log1 + log2 + .. logn which is approximately nlog(n) cause first we create a heap of size n, and then pop from it k times. So the totoal time complexity is O(n.log(n) + log(n).k) which is equal to O(nlog(n)). the second part added in the complexity is from removing k elements from the heap of size n. However for a min-heap implementation since our heap is max of size k the complexity is O(n.log(k))
- [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)
	- Concepts : #HashMaps #Hash-Table #PriorityQueues
	- Approach : We use the freqMap to track the frequency. Then we iterate the unique elements with their freq to populate the min-heap with the k most frequent elements.
	- Learnings :
		- map.computeIfPresent(nums[i], (key, freq) -> freq+1);  : This helps update the frequency.
		- map.computeIfAbsent(nums[i], (key) -> 1); Helps populate absent element with frequency 1
	- Status : Solved
- [Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/)
	- Concepts : #PriorityQueues 
	- Approach : The logic is that for median we need the largest of the small values and smallest of the largest values to calculate the mean in case of equal number of values in both baskets, or else it is the odd value in either basket. We use this basis to use the priority queue logic to solve the problem.
	- Status : Solved
- [K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/)
	- Concepts : #PriorityQueues 
	- Approach : Maintain a max priority queue using the distance as organising factor, and accordingly store. By using the max heap we are maintaining the smallest k points based on distance by replacing the root with smaller value whenever encountered.
	- Learnings :
		- For the comparator we supply it in the constructor () brackts of PriorityQueue
			- eg. PriorityQueue pq = new PriorityQueue ((a, b) -> (b-a)) : this is descending
			- for the points we do PriortyQueue pq = new PriortyQueue ((a, b) -> (b.distance() - a.distance()))
		- Also for points java has a class Point with import java.awt.Point;
	- Status : Solved
- [Task Scheduler](https://leetcode.com/problems/task-scheduler/)
	- Concepts : #Greedy #PriorityQueues 
	- Approach : Maintain a priority queue as we need to prioritise getting the most frequent elements first. This ie because this allows to add other elements in the middle to try to reduce the idle time. Also once we get that, we maintain a common timer, which increases and also our pair structure needs a time field to know when the current pair will be available again. We use this to add it back to the pq to process again. during the idle time, we use a q to maintain the FIFO principle for the waiting tasks as they will become available to be re run in the order they were worked on.
	- Learnings:
		- We need the time stamp as if we keep a common one, say in the sample a,a,a,b,b,b when t = 3, a gets used again but at that b is also already there, which should become available now. for the next iteration. so having the time stamp helps to do that. also after processing a current node also we need to see if any node can be added back in the same we need to see if they are added back after an idle run.
	- Status : Solved
- [Reorganize String](https://leetcode.com/problems/reorganize-string/)
	- Concepts : #Greedy  #PriorityQueues 
	- Approach : We can use the same logic of task scheduler where the cooldown in 1, as they aren't allowed to be consecutive and use that logic to populate the string. This way if we ever come across the situation where the pq is empty() that means an idle is needed or a char has to be repeated, and hence we can return an empty string. or else we can continue to populate the string.
	- Learnings : 
		- We can use a StringBuilder to add char at each step to keep it as O(1) operation as otherwise as string is not mutable it becomes an O(N) job to make a new string. and in the end we can do stringBuilderInstance.toString() to convert it to a string.
	- Staus : Solved
- [Sort Characters By Frequency](https://leetcode.com/problems/sort-characters-by-frequency/)
	- Concepts : #Greedy #PriorityQueues #Bucket-Sort
	- Approach : 
		- PriorityQueue : We can store the character ,frequency in a class and maintain a priorityQueue to keep track of most frequent one, and then keep popping and building the string with the frequency stored to reconstruct the string 
		- Bucket Sort : Since we have a limit for the frequency, we can make a List of Character array where the index is the frequency and the list at each index contains the chars with that frequency. Then we can iterate this list in reverse to get the max frequency elements to populate the result string.
	- Learnings : 
		- Since the frequency has a fixed range we can use the bucket sort method here too.
	- Status : Solved
- [Top K Frequent Words](https://leetcode.com/problems/top-k-frequent-words/)
	- Concepts : #PriorityQueues 
	- Approach : 
		- Priority Queue : You can define a custom comparator to you priorityQueue using the code shown below to handle ties and then put all map entries into the Priority Queue and them pop k values to get them in the right orders.
			- ```Java
			  PriortiyQueue<Map.Entry<String, Integer>> pq = new PrioritQueue<>(
				  Map.Entry.<String,Integer>
				  comparingByValue(Comparator.reverseOrder()).
				  thenComparing(Map.Entry.comparingByKey())
				  );
			  ```
		  - Priority Queue with limit at k : We have to reverse the list comparator cause we want the result in reverse. So we keep a min heap and store the lexicographically larger word first. this helps get the smallest values rid first. 
	- Learnings : 
		- The Priority Queue is needed in reverse order lexicographically cause among the smaller frequency we need the candidates which have smaller lexicographical values.
-  [IPO](https://leetcode.com/problems/ipo/)
	- Concepts : #PriorityQueues 
	- Approach : We use to Priority Queue, one is a min heap based on cost to be able to get all the possible candidates now allowed to be added to out affordable Priority Queue. The affordable Priority Queue is a max heap based on the profits. this way we first add all our affordable candidates to the affordable queue by using the increasing property if the min heap to add them and stop as all subsequent ones would be higher values of cost which we yet cannot afford. Also the max heap at affordable at every instant helps us to get the max value project in terms of profit in O(1) at every instance.
	- Status : Solved
- [Meeting Rooms II](https://leetcode.com/problems/meeting-rooms-ii/)
	- Concepts : 
	- Approach :
		- Brute Force Approach : We do a O(N^2) approach where for each interval we see if it has an overlap with another meeting interval, and then accordingly increase the count of the rooms. Now each meeting needs a room for itself, so we keep instantiated as one.
		- Optimised Approach : We first sort the intervals according to starting point and then ending time. We can then iterate over them and maintain a min heap of the ending times, this way we can see with how many existing meeting we are conflicting. also since the starting points are sorted, future starting points encountered are greater than given value so we can remove all ending times smaller than current start time as they would never have a conflict with another meeting as well.
	- Learnings : 
		- We need two heaps, one to keep track of roomAvailable, and also a time, room heap where its sorted on basis of time, and then room. this helps us to get only one room which is needed rather than freeing all rooms that might not be required.
		- The code to sort the intervals :  
			- ```Java
					Arrays.sort(intervals,
						Comparator.comparingInt((int[] a) -> a[0])
					              .thenComparingInt(a -> a[1])
					);
			  ```
	- Status : Solved