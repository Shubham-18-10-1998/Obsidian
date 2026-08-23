
# Introduction
							
							Insertion                     Search
Unsorted Array                                        O(1)                                                   O(N)
Sorted Ray                                               O(N)                                                  O(log(N))
Stack                                                        O(1)                                                    O(N)
Heap                                                         O(log(N))                                          O(N.log(N))
Linked List                                                O(1)                                                   O(N)
Hash-Map                                                O(1)                                                    O(1)



Hash-Map : Key-Value Pairs data-structure
Searching for a key is -> O(1)

Tree-HashMap : The keys are also sorted

# HashMap — Internal Implementation & Interview Notes

## 1. What is a HashMap?

A HashMap stores data as:

    key → value

Example:

    "Alice" → 25
    "Bob"   → 31
    "John"  → 42

The goal is to provide approximately O(1) average-time lookup, insertion, and deletion.

---

# 2. How does HashMap work?

The basic idea is:

    Key
     ↓
    hashCode()
     ↓
    hash
     ↓
    bucket index
     ↓
    find entry
     ↓
    compare keys using equals()
     ↓
    return value

Instead of searching through every key, the hash allows us to jump to the bucket where the key should be.

This is why HashMap can provide O(1) average lookup.

---

# 3. Buckets

A HashMap internally has an array of buckets.

Conceptually:

    Bucket 0
    Bucket 1
    Bucket 2
    Bucket 3
    Bucket 4
    ...

A simplified bucket calculation could be:

    bucket = hash % numberOfBuckets

Example:

    hash("Alice") = 12
    numberOfBuckets = 5

    12 % 5 = 2

Therefore:

    Alice → Bucket 2

---

# 4. Hash Collisions

A collision occurs when multiple different keys map to the same bucket.

Example:

    Alice → hash 12 → bucket 2
    Bob   → hash 7  → bucket 2
    John  → hash 22 → bucket 2

So:

    Bucket 2
       ↓
    Alice
    Bob
    John

Different keys can have the same bucket.

A collision is normal and expected in a HashMap.

---

# 5. How are collisions handled?

Conceptually, entries in the same bucket can form a chain/list:

    Bucket 2
       ↓
    Alice → Bob → John

When looking up a key, HashMap finds the bucket and then checks the entries inside that bucket.

If the bucket becomes heavily populated, modern Java HashMap can convert the bucket into a Red-Black Tree.

Conceptually:

              Alice
             /     \
           Bob     John

This can improve lookup within that heavily-collided bucket from O(n) to approximately O(log n).

Important:

HashMap is NOT normally a collection of trees.

Normally, buckets contain very few entries.

Treeification is primarily a mechanism for handling heavy collisions.

---

# 6. HashMap get()

Suppose:

    map.get("Alice")

Conceptually:

    "Alice"
       ↓
    hashCode()
       ↓
    determine bucket
       ↓
    inspect candidate entries
       ↓
    compare keys
       ↓
    return value

The key comparison is important because two different keys can have the same hash.

---

# 7. hashCode() vs equals()

HashMap uses both:

    hashCode()
    equals()

### hashCode()

Used to determine where the key should be looked up.

    key
     ↓
    hashCode()
     ↓
    bucket

### equals()

Used to determine whether two keys are actually considered equal.

For example:

    Person("Alice")
    Person("Alice")

They may have the same data but still be different objects.

---

# 8. The equals() / hashCode() Contract

Very important Java interview rule:

If:

    a.equals(b) == true

then:

    a.hashCode() == b.hashCode()

must also be true.

However:

    a.hashCode() == b.hashCode()

does NOT guarantee:

    a.equals(b) == true

because different objects can have the same hash code.

Example:

    Alice → hash 42
    Bob   → hash 42

But:

    Alice.equals(Bob) == false

This is a hash collision.

---

# 9. Example with Person

Suppose:

    class Person {
        String name;
    }

and:

    Person p1 = new Person("Alice");
    Person p2 = new Person("Alice");

If we do not override equals() and hashCode():

    p1.equals(p2) → false

because the default Object equality is based on object identity.

Therefore:

    map.put(p1, 100);

    map.get(p2);

will not find p1's entry and will return:

    null

---

## Correct implementation

If we override:

    equals()

to compare names:

    p1.equals(p2) → true

and override:

    hashCode()

so equal names produce the same hash:

    p1.hashCode() == p2.hashCode()

then:

    map.put(p1, 100);

    map.get(p2);

returns:

    100

---

# 10. HashMap Complexity

Typical/average complexity:

    get()         → O(1)
    put()         → O(1)
    remove()      → O(1)
    containsKey() → O(1)

Why?

Because hashing allows us to approximately jump directly to the correct bucket.

---

# 11. Worst-Case Complexity

HashMap is not guaranteed to be O(1) in every situation.

If many keys collide into the same bucket, lookup can degrade.

Conceptually, with a long chain:

    Bucket
      ↓
    A → B → C → D → E

Lookup could become:

    O(n)

Modern Java HashMap can treeify sufficiently large collision-heavy buckets using a Red-Black Tree.

Then lookup within that bucket can be approximately:

    O(log n)

Interview answer:

> HashMap operations are O(1) on average. Heavy collisions can degrade performance, and modern Java can treeify sufficiently large collision chains, giving approximately O(log n) lookup within that bucket.

---

# 12. Load Factor

Load factor measures how full the HashMap is.

Simplified:

    Load Factor =
        number of entries
        -----------------
        number of buckets

Example:

    6 entries
    8 buckets

    Load Factor = 6 / 8
                = 0.75
                = 75%

A high load factor means more entries per bucket and therefore a higher probability of collisions.

---

# 13. Resizing

When the HashMap becomes too full, it increases the number of buckets.

Example:

    Before:

    8 buckets

    ↓ resize

    After:

    16 buckets

Existing entries need to be redistributed because the bucket calculation depends on the bucket-array size.

For example:

    hash = 12345

Before:

    12345 % 8
    → bucket 1

After:

    12345 % 16
    → bucket 9

The hashCode itself does not necessarily change.

The mapping from hash → bucket changes because the number of buckets changed.

---

# 14. Why resize?

More buckets means:

    fewer entries per bucket
            ↓
    fewer collisions
            ↓
    faster average lookup

This is similar to ArrayList resizing:

    ArrayList:
    capacity becomes full
          ↓
    allocate larger array
          ↓
    copy elements

HashMap:

    Map becomes too full
          ↓
    allocate larger bucket array
          ↓
    redistribute entries

---

# 15. Amortized Complexity of HashMap

A resize is an expensive operation because many existing entries may need to be redistributed.

Therefore, an individual operation that triggers resizing can be expensive.

However, resizing happens only occasionally.

Therefore:

    Normal get/put/remove → O(1) average

while:

    Resize → O(n) work

The overall average behavior remains approximately:

    O(1)

---

# 16. Important Mental Model

Think of HashMap as:

                    HashMap
                       |
                Array of buckets
                       |
                 hashCode(key)
                       |
                 bucket selection
                       |
              ┌────────┴────────┐
              ↓                 ↓
        Few collisions      Heavy collisions
              ↓                 ↓
        entries/chain       Red-Black Tree
              ↓                 ↓
           equals()        equals()/tree lookup

Average:

    O(1)

Heavy collision bucket:

    approximately O(log n) with treeification

---

# 17. HashMap vs ArrayList

ArrayList:

    Search → O(n)

because you may need to inspect every element.

HashMap:

    Search by key → O(1) average

because hashing lets you jump to the relevant bucket.

Trade-off:

    HashMap
    → faster lookup
    → extra memory
    → no inherent sorted ordering

    ArrayList
    → compact/sequential storage
    → O(1) index access
    → O(n) search

---

# 18. HashMap vs TreeMap

HashMap:

    get() → O(1) average
    put() → O(1) average

    Keys sorted?
    No

TreeMap:

    get() → O(log n)
    put() → O(log n)

    Keys sorted?
    Yes

Use TreeMap when you need:

- Sorted keys
- Range queries
- Smallest/largest key
- Floor/ceiling operations
- Ordered traversal

---

# 19. HashMap vs HashSet

HashMap:

    key → value

HashSet:

    value

Use HashMap when you need:

    key → associated value

Use HashSet when you only need:

    "Have I seen this value?"

Example:

    Set<Integer> seen = new HashSet<>();

    seen.contains(x) → O(1) average
    seen.add(x)      → O(1) average

---

# 20. Interview Questions You Should Be Able to Answer

### Why is HashMap O(1) average?

Because hashing allows us to determine the bucket where a key should be stored/looked up without scanning all entries.

### Why isn't HashMap guaranteed O(1)?

Because multiple keys can collide into the same bucket.

### What is a collision?

Two different keys map to the same bucket.

### How are collisions handled?

Entries in the bucket can be chained; modern Java can treeify heavily-collided buckets into a Red-Black Tree.

### Why do we need equals()?

Hash codes can collide, so equals() is used to determine whether two keys are actually equal.

### Why do we need hashCode()?

It helps determine which bucket should be searched.

### What is the equals/hashCode contract?

If:

    a.equals(b) == true

then:

    a.hashCode() == b.hashCode()

must be true.

### Why does HashMap resize?

To increase the number of buckets, reduce collisions, and maintain efficient average lookup.

### Does resizing change hashCode()?

Not necessarily.

The key's hash code can remain the same. The bucket calculation changes because the number of buckets changes.

### What is load factor?

Approximately:

    entries / buckets

It indicates how full the HashMap is.

---

# 21. One-Line Mental Model

Remember:

    HashMap =
    hashCode()
    + bucket array
    + collision handling
    + equals()
    + resizing
    + load factor

The goal is:

    O(1) average lookup/insertion/deletion

# Problems
- [Two Sum](https://leetcode.com/problems/two-sum/)
	- Approach : With Hash-Map we use the map to keep value and index in key value pair, Then we iterate through map if for any index where we have target-nums[i] also exists in the map, we populate the array and break the loop, else we add the key-value pair.
	- Status : Solved
- [4Sum II](https://leetcode.com/problems/4sum-ii/)
	- Initial Approach : We make a frequency map for values in last array
	- Approach : Supposed to do for two arrays sum at one time to create sum frequency map.
	- Learnings : 
		- map.getOrDefault(sum, 0)
		- Approach
	- Status : Unsolved
- [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)
	- Approach : Use prefix sum to optimise the code, and then use hash-map to maintain frequency to solve
	- Learnings : cant keep res++ for sum equal to k as it needs to know all values before it for which the sub-sum is 0.
	- Status : Unsolved
- [Ransom Note](https://leetcode.com/problems/ransom-note/)
	- Approach : Use a int[] of length 26 as map for both magazine and ransomNote to maintain char count. Once poulated for both. iterate through the two arrays and if map_ransomNote[i] > map_mag[i] then return false, cause then it cant be constructed or else return true.
	- Status : Solved
- [Valid Anagram](https://leetcode.com/problems/valid-anagram/)
	- Approach : create an int array of length 26 to function as map for string s. Put check if they are of unequal length, then return false. When iterating through t, before reducing count check if the count in map there is already 0 return false, or else reduce count and continue. if you are able to iterate through the loop, then it will be all zeroes in the end as they are of same length and no count went into negative. Hence after loop return true.
	- Learnings:
		- For the array frequency map, we can maintain just one array and for string s increase the count of frequency, and for string t, reduce the frequency. By doing this, in the end if the frequency for an element is 0 the it was either equally present in the anagram, or it wasn't present at all which is also okay, however if it is non-zero, then there is an unequal amount of this character in the two string, and hence its not an anagram.
	- Status : Solved
- [Longest Palindrome](https://leetcode.com/problems/longest-palindrome/)
	- Approach : Use a map to iterate through the string and update frequency of each character. Now we are allowed at most one odd frequency (as this can come in the centre and still be palindrome) and rest all should be even hence we can add for all others freq - (freq%2).
	- Learnings :
		- map.merge(key, 1, Integer::sum) is used to increase freq of chars by one and instantiate with 1.
		- mag.values() gives iteratable for all values of map
- [Roman to Integer](https://leetcode.com/problems/roman-to-integer/)
	- Approach : Create a map<Character, int[]> for storing priority and value for each char, and then iterate from the back. If priority cur < priority prev, then value is subtracted, or else value is added.
	- Learnings : 
		- Don't need priority as the priority is same as value and that can directly be used. Hence we only need a map for <char, int>. Also we can use int[128] as ASCII values range from 0 to 127.
	- Status : Solved
- [Time Based Key-Value Store](https://leetcode.com/problems/time-based-key-value-store/)
	- Concepts : #Hash-Table #String #BinarySearch #Design 
	- Approach : Used a map of String, Deque<Pair<String, Integer>>. This was we have notion of min value using getFirst() of Deque, and max element using getLast(). Also in case its between them, then we use a descending iterator to get the value in between.
	- Learnings : 
		- For Iterator i.next() returns Object. So to resolve this, we make Iterator<Pair<String, Integer>>. And then use i.next() once to get the pair we are on now. And then use the values to compare.
	- Optimal Solution : We store the values as map<key, List<Pair<Integer, String>>. This was we can use binary search to utilise the constraint that values are strictly increasing.
	- Status : Solved

Questions : 

1. **https://leetcode.com/problems/longest-consecutive-sequence/description/**

2. https://leetcode.com/problems/top-k-frequent-elements/description/

3. https://leetcode.com/problems/two-sum/description/

4. **https://leetcode.com/problems/4sum/**

5. **https://leetcode.com/problems/contains-duplicate/description/**

6. **https://leetcode.com/problems/valid-anagram/description/**
