Logic for n-1 iterations in these sorting algorithms: A n element array can be fully sorted if it contains of two sub arrays one having one element thats unsorted and another with n-1 elements which are sorted with the logic that if you have n-1 elements sorted in right place, then the other elements automatically lands in the right place which causes all elements to be sorted.

# Bubble Sort
## Logic
Push the largest element to the end of the array by swapping between adjacent elements.
Every iteration i, the i-th element from end are in the sorted (correct) place.
## Code
https://www.geeksforgeeks.org/problems/bubble-sort/1
## Learning:
Here n-1 in first loop cause we can assume we are stating with an unsorted array from 0 -> n-2 elements, and n-1 element is sorted. Then we go from 0 ->  n-1-i for j loop (inside loop) cause that many elements are now sorted. ie. The elements from n-i -> n-1 are already sorted.

# Selection Sort
## Logic
Consider two parts, one sorted and one un-sorted. Figure out min element in unsorted array and swap with first index of un-sorted array. Then in next iteration, the 1 is now part of sorted part and do the same (find min element and replace with 1st element in unsorted array). Keep doing this n-1 time.
- Not the opposite of bubble sort as here swapping adjacent elements doesn't ensure the min of array is now in first place.
	- Also here only one swap per iteration but there many swap per iteration.
## Code
https://www.geeksforgeeks.org/problems/selection-sort/1
## Learning:
- Initially keep a separate minValue variable but wasn't updating that during the comparison, which was resulting in the wrong answer;

# Insertion Sort
##  Logic - 
Consider the process of you adding a card to your hand and having the cards in your hand sorted in a given order (ascending or descending). Insertion sort works the same way. We start with a sorted array of one element, and each new element is then added to its correct place in the subarray of (0 -> i) where i is the index of the element in the array. This then maintains a sorted array for the indices 0 -> i.
- Difference from selection sort : There in each iteration you find the smallest element in the remaining subarray (i -> n) and bring it to the start. And that was you get a sorted array from index 0 -> i. However here you keep a maintain a sorted array from 0->i by sorting the particular sub-array till that index.
- Can be considered the opposite of bubble sort in the sense that you have a sub-array in insertion sort from 0->i and there you have sub-array from n-i -> n. But the difference is that here the subarray consists of elements in the original unsorted array but they are now sorted. However in the bubble sort its the elements for the whole array that are the largest.
## Code :
https://www.geeksforgeeks.org/problems/insertion-sort/1


