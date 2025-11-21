Continuous block of memory that stores some homogenous kind of data.

- [Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
	- Initial Approach : 2 For loops, and check every possibility
	- Learning - For Sub-array, the new Element is the max Sub-array if curSum (cumulative max is lesser than 0), or else if curSum > 0, then it can contribute t increase the maxSum sub-array.
- [Two Sum](https://leetcode.com/problems/two-sum/)
	- Initial Approach: Use a hash-Map with index and then sort the hash-map. use two pointers to check sum, if greater then reduce back-pointer and if smaller then increase forward-pointer.
	- Learning : Cant sort hash-map as for sort function in cpp to run, as for sort to work it needs random-access iterator which hash-map (unordered_map) doesn't provide.
		- Hence Use vector of pair of int and then solve it using the same logic. This also resolves issue of duplicate elements in parent array which would cause issue in unordered_map as there key has to be unique.
- [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)
	- Initial Approach: Sort the array and check adjacent indices for same value
- [Count Hills and Valleys in an Array](https://leetcode.com/problems/count-hills-and-valleys-in-an-array/)
	- Initial Approach: Use a prevUniq to keep track of prev non-equal element to compare to find occurrence of hill or valley.
- [Number of Laser Beams in a Bank](https://leetcode.com/problems/number-of-laser-beams-in-a-bank/)
	- Initial Approach: Use a prevEmpty flag to keep track of empty rows. However when test case failed realised we don't need to keep that as two continuous rows with lasers devices will have beams between themselves too.
- [Make Array Elements Equal to Zero](https://leetcode.com/problems/make-array-elements-equal-to-zero/)
	- Initial Approach: Use recursion to simulate the process and get solutions. This is essentially brute force and was leading Time Limit Exceeded error.
	- Learning: If the sum of elements on either side of 0 is equal, then count increases by 2. Or else if sum difference is 1, then we increase by as the sum should be equall to get the condition of all zeroes ultimately. Because problem can thought of dominoes each following 1 by 1 on either sides. and you can escape only if number of dominoes on either side is equal.
- [The Two Sneaky Numbers of Digitville](https://leetcode.com/problems/the-two-sneaky-numbers-of-digitville/)
	- Use a hash-map to store frequency and if frequency is equal to 2, then add to res array.
- [Third Maximum Number](https://leetcode.com/problems/third-maximum-number/)
	- Initial Approach : First sorted the array and the traversed till 3rd unique element found. Initially didn't realise sorting is done in ascending order, but here descending order is needed.
	- Learning :
	- `int[]` to `Integer[]` Conversion: 
    
	    The `Arrays.sort()` method with `Collections.reverseOrder()` as a comparator only works with object arrays (like `Integer[]`, `String[]`, etc.), not primitive arrays (`int[]`). Therefore, you need to convert the `int[]` to `Integer[]`. This is done using `Arrays.stream(primitiveArray).boxed().toArray(Integer[]::new)`.
    
	    - `Arrays.stream(primitiveArray)` creates an `IntStream` from the `int[]`.
	    - `.boxed()` converts the `IntStream` to a `Stream<Integer>`.
	    - `.toArray(Integer[]::new)` collects the elements into an `Integer[]`array.
    
	- **Sorting in Descending Order:** 
    
	    `Arrays.sort(objectArray, Collections.reverseOrder());` sorts the `Integer[]` in descending order.`Collections.reverseOrder()` provides a `Comparator` that reverses the natural order of elements.
    
	- `Integer[]` to `int[]` Conversion (Optional): 
    
	    If you need the result back in a primitive `int[]` array, you can convert the sorted `Integer[]` back using `Arrays.stream(objectArray).mapToInt(Integer::intValue).toArray()`.
    
	    - `Arrays.stream(objectArray)` creates a `Stream<Integer>`.
	    - `.mapToInt(Integer::intValue)` maps each `Integer` object back to its primitive `int` value, creating an `IntStream`.
	    - `.toArray()` collects the elements into an `int[]` array.
- [1-bit and 2-bit Characters](https://leetcode.com/problems/1-bit-and-2-bit-characters/)
	- Initial Thinking : If i trying going from the back to evaluate and see if string is valid, then can find.
	- Learning : start a loop from i=0, if num == 1, then skip two, or else skip 1, if you end on the last char somehow, (which has to be a 0), then its a valid string, if you don't, that mean that last 0 part of 2 symbol character, and hence value is false.
- [Keep Multiplying Found Values by Two](https://leetcode.com/problems/keep-multiplying-found-values-by-two/)
	- Initial Approach : Keep a set to track all values. Then keep the flag true till value of 2 x original is found in set and update value of original.
- [Largest Number At Least Twice of Others](https://leetcode.com/problems/largest-number-at-least-twice-of-others/)
	- Initial Approach : Sort and check the last indices to see if condition is satisfied.
	- Learning : Instead can keep two variables, largest and second largest . When largest updated, old largest becomes second largest. Or else check is value greater than second largest. Then after iterating array check the condition through these variables.