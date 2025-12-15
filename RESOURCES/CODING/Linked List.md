
Important conditions
- always add null check


# What is Linked List?
Collection of nodes
- First element of list is called head.
- Last element is called tail

## Types of linked list
- Singly linked list
- Circular linked list (here tail.next = head)
- Doubly linked list (has prev and next in node)

## What is a node?
A class with information
- Data : Can be anything
- Pointers
	- Forward : Reference for next
	- Backward : Reference for previous

## Why do we need a linked list?
- Memory allocation in heap with arrays etc. This is contiguous data block. However with linked list, the nodes can be at random places with no location to each other.
- Allows to give dynamic size as new element can be attached to last.
- Insertion at head or tail is O(1) if tail maintained.


# Problems
- [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)
	- Learnings : Use a pen and paper to visualise
- [Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/)
	- Learnings : 
		- slow and fast pointer
		- Note : Try for first middle event in case of even.
- [Linked List Insertion At End](https://www.geeksforgeeks.org/problems/linked-list-insertion-1587115620/0)
	- Learnings :
		- checks for null head
		- Always use iterator instead of operating head as we need to keep address of head always
- [Find Length of Linked List](https://www.geeksforgeeks.org/problems/count-nodes-of-linked-list/0)
	- Learnings :
		- Initially check for null header.
		- Update length by incrementing while we keep doing cur = cur.next.
- [Delete Node in a Linked List](https://leetcode.com/problems/delete-node-in-a-linked-list/)
	- Learnings:
		- Since we don't have head, we cant manipulate the addresses to change links(That is the pointers). Hence we change the values  with existing link. and keep a prev to track the last node of updated list whose next is then updated to null.
- [Search in Linked List](https://www.geeksforgeeks.org/problems/search-in-linked-list-1664434326/1)
	- Approach : Keep an itr which initially points to head, In the loop check while itr != null, if the value is found, or else go to the next value. If all values checked without finding key then value doesn't exist.
- [Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)
	- Approach : Decide the head first, as if one of the list is null we can just return the other list this also helps to return the head in the end. Then keep two pointers, one for itr, one for prev, and manipulate the prev.next to itr now chosen and before assigning the node, make list = list.next for the respective list who node has been chosen.
- [Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)
	- Approach : Create a new linked list with head, cur to point to current node being operated on, and a prev to keep track of previous node. This prev plays a crucial role in case of carry over for last node value. IN case if carry is 1, the cur gets a val of 1 or else prev.next becomes null.
	- Learnings :
		- make sure to move the l1 and l2 to next values.
		- Use a prev to track the penultimate tail node of linked list.
		- use a carry to track the carry over.
- [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)
	- Approach : use a hash-set for the nodes. As it doesn't store duplicate values then in case we cycle and trying adding the value we will get a false for addition.
	- Learning : 
		- add() for hash-set returns a boolean to show if value was added or not.
		- since head isn't allowed to be null for loop condition, set null doesn't interfere with the logic.


Questions -
1. https://www.geeksforgeeks.org/problems/linked-list-insertion-1587115620/0

2. https://www.geeksforgeeks.org/problems/count-nodes-of-linked-list/0

3. https://leetcode.com/problems/delete-node-in-a-linked-list/description/

4. https://www.geeksforgeeks.org/problems/search-in-linked-list-1664434326/1

5. https://leetcode.com/problems/reverse-linked-list/description/

6. https://leetcode.com/problems/merge-two-sorted-lists/description/

7. **https://leetcode.com/problems/add-two-numbers/description/**

8. **https://leetcode.com/problems/linked-list-cycle/description/**
