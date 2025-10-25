
# Bubble Sort
## Logic
Push the largest element to the end of the array by swapping between adjacent elements.
Every iteration i, the i-th element from end are in the sorted (correct) place.

# Selection Sort
## Logic
Consider two parts, one sorted and one un-sorted. Figure out min element in unsorted array and swap with first index of un-sorted array. Then in next iteration, the 1 is now part of sorted part and do the same (find min element and replace with 1st element in unsorted array). Keep doing this n-1 time.
- Not the opposite of bubble sort as here swapping adjacent elements doesn't ensure the min of array is now in first place.
	- Also here only one swap per iteration but there many swap per iteration.
