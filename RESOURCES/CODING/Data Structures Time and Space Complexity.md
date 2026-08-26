
# Summary
| Structure | Main Use | Key Operations |
|---|---|---|
| ArrayList | Random access | get O(1), append O(1) amortized |
| LinkedList | Node/end operations | end operations O(1) |
| Stack | LIFO | push/pop/peek O(1) |
| Queue | FIFO | offer/poll/peek O(1) |
| Deque | Both ends | end operations O(1) amortized |
| ArrayDeque | Java Stack/Queue/Deque | Efficient circular-array implementation |



# Data Structures — SDE2/SDE3 Interview Notes

## 1. Array

An array has a fixed size and stores elements in contiguous memory.

### Time Complexity

| Operation | Complexity | Why |
|---|---:|---|
| Access by index | O(1) | Direct address calculation |
| Search | O(n) | May need to inspect every element |
| Insert at beginning | O(n) | Existing elements must be shifted |
| Insert in middle | O(n) | Elements must be shifted |
| Insert at end | O(1)* | If capacity/space already exists |
| Delete from beginning | O(n) | Remaining elements must be shifted |
| Delete from middle | O(n) | Remaining elements must be shifted |
| Delete from end | O(1) | No shifting required |

> Arrays do not automatically resize. If a larger array must be allocated and elements copied, that operation is O(n).

---

# 2. ArrayList

`ArrayList` is backed by a **dynamic array**, NOT a linked list.

Conceptually:

    [A][B][C][D][_][_][_]

It maintains a contiguous array and grows when necessary.

                 ArrayList
                    |
             Dynamic Array
                    |
        ┌───────────┴───────────┐
        ↓                       ↓
    size                    capacity
(actual elements)                       (allocated space)

        Dynamic Array
             ↓
      Fast random access
             ↓
          O(1) get
             ↓
    Expensive middle insertion
             ↓
           O(n)

### Time Complexity

| Operation | Typical Complexity |
|---|---:|
| `get(i)` | O(1) |
| Search | O(n) |
| Insert at beginning | O(n) |
| Insert in middle | O(n) |
| `add(element)` at end | Amortized O(1) |
| Remove from beginning | O(n) |
| Remove from middle | O(n) |
| Remove from end | O(1) |

### Why is `add()` at the end amortized O(1)?

Most insertions simply place the element at the next available position:

    [A][B][C][D][_]
                 ↑
                add

This is O(1).

Occasionally the backing array becomes full:

    [A][B][C][D]

A larger array must be created and the existing elements copied:

    Old array → New larger array

That particular insertion costs O(n).

However, resizing happens infrequently, so over a large number of insertions:

    Amortized complexity = O(1)

Important distinction:

- Typical insertion at end = O(1)
- Worst-case individual insertion = O(n)
- Amortized insertion = O(1)

---

# 3. LinkedList

A LinkedList stores elements as nodes connected by references.

For a doubly linked list:

    A <-> B <-> C <-> D

Each node contains references to the previous and next node.

      Nodes + pointers
             ↓
     No random access
             ↓
          O(n) get
             ↓
    Fast insertion/deletion
         if node reference exists
             ↓
            O(1)

### Time Complexity

| Operation | Complexity |
|---|---:|
| Access by index | O(n) |
| Search | O(n) |
| Insert at beginning | O(1) |
| Insert at end | O(1)* |
| Delete from beginning | O(1) |
| Delete from end | O(1)* |
| Insert after known node | O(1) |
| Delete known node | O(1) |

\* Assuming the implementation maintains references to the relevant end.

### Why is insertion at index i O(n)?

Suppose:

    A <-> B <-> C <-> D <-> E

To insert after B, if we already have a reference to B:

    Find B → already done
    Insert new node → O(1)

But if we are told:

    insert at index 1,000

we first need to traverse the list to find that position.

    Find node → O(n)
    Insert → O(1)

Therefore:

    Total = O(n) + O(1)
         = O(n)

### Key Interview Point

LinkedList insertion/deletion is only O(1) **once you already have the node/reference**.

Finding the location can still cost O(n).

---

# 4. Array vs ArrayList vs LinkedList

| Operation | Array | ArrayList | LinkedList |
|---|---:|---:|---:|
| Access by index | O(1) | O(1) | O(n) |
| Search | O(n) | O(n) | O(n) |
| Insert beginning | O(n) | O(n) | O(1) |
| Insert middle | O(n) | O(n) | O(n)* |
| Insert end | O(1)** | Amortized O(1) | O(1) |
| Delete beginning | O(n) | O(n) | O(1) |
| Delete middle | O(n) | O(n) | O(n)* |
| Delete end | O(1) | O(1) | O(1) |

\* Finding the node costs O(n), but the actual insertion/deletion once the node is known is O(1).

\** Assuming available space.

### Practical Rule

Use:

    Array / ArrayList
    → When you need fast random access

    LinkedList
    → When you frequently insert/delete at known positions/nodes

In practice, `ArrayList` is often preferred over `LinkedList` because of better cache locality and lower memory overhead, unless the linked-list behavior is specifically useful.

---

# 5. HashMap

A HashMap stores key-value pairs:

    key → value

Example:

    "Shubham" → 123
    "John"    → 456

A hash function converts the key into a bucket/index.

    key
     ↓
    hash
     ↓
    bucket
     ↓
    value

HashMap
   ↓
hashCode()
   ↓
hash function / bucket index
   ↓
collision
   ↓
collision resolution
   ↓
load factor
   ↓
resize / rehash
   ↓
Java HashMap treeification

### Average Complexity

| Operation | Average |
|---|---:|
| `put()` | O(1) |
| `get()` | O(1) |
| `remove()` | O(1) |
| `containsKey()` | O(1) |

### Why is HashMap O(1) on average?

A good hash function distributes keys across buckets.

Ideally:

    key → hash → bucket → element

So we don't need to search the entire collection.

---

## Hash Collisions

Two different keys can map to the same bucket.

    Key A ──┐
            ├──> Bucket 5
    Key B ──┘

This is called a collision.

If many keys collide, lookup becomes slower.

Conceptually, a heavily-collided bucket could require:

    O(n)

lookup.

Modern Java HashMap can convert sufficiently large collision chains into a balanced tree, improving that bucket's lookup to approximately:

    O(log n)

### Interview Answer

> HashMap get/put/remove are O(1) on average because hashing provides direct access to a bucket, assuming good hash distribution. Heavy collisions can degrade performance, and modern Java can treeify sufficiently large collision chains, giving approximately O(log n) lookup within that bucket.

---

# 6. HashSet

HashSet stores unique values.

Example:

    Set<Integer> seen = new HashSet<>();

Useful operations:

    seen.contains(x)
    seen.add(x)
    seen.remove(x)

Average complexity:

    contains → O(1)
    add      → O(1)
    remove   → O(1)

### HashSet vs HashMap

Use HashSet when you only need:

    "Have I seen this value?"

Use HashMap when you need:

    "What value is associated with this key?"

Example:

    HashSet:
    5 → exists?

    HashMap:
    5 → "Alice"

### Interview Rule

> Choose the simplest data structure that provides the operations you need.

---

# HashSet — Internal Implementation & Interview Notes

## 1. What is a HashSet?

A HashSet stores **unique values**.

Example:

    Set<Integer> set = new HashSet<>();

    set.add(10);
    set.add(20);
    set.add(10);

The final Set contains:

    10
    20

The second `10` is not added because Sets do not allow duplicates.

---

# 2. Core Idea

A HashSet is primarily used for:

    Membership
    Uniqueness
    Duplicate detection

Typical questions:

    "Have I seen this value before?"

    "Does this value already exist?"

    "Does the collection contain duplicates?"

For these problems, HashSet is usually a natural choice.

---

# 3. HashSet is built on HashMap

In Java, HashSet is implemented using a HashMap internally.

Conceptually:

    HashSet

    value
      ↓
    HashMap key

For example:

    set.add("Alice");

can conceptually be thought of as:

    HashMap:

    "Alice" → PRESENT

Then:

    set.add("Bob");

becomes:

    "Alice" → PRESENT
    "Bob"   → PRESENT

The actual Java implementation has additional details, but the important mental model is:

    HashSet cares about the keys.
    The HashMap's values are not meaningful to the Set.

---

# 4. How does HashSet detect duplicates?

Suppose:

    set.add("Alice");

The process is conceptually:

    "Alice"
        ↓
    hashCode()
        ↓
    determine bucket
        ↓
    inspect existing entries
        ↓
    equals()
        ↓
    ┌───────────────┐
    ↓               ↓
  Equal          Not equal
    ↓               ↓
 Don't add       Add element

Therefore HashSet relies on:

    hashCode()
    equals()

just like HashMap keys.

---

# 5. HashSet Complexity

Average/typical complexity:

    add()      → O(1)
    contains() → O(1)
    remove()   → O(1)

These are average-case complexities because they depend on good hash distribution.

HashSet is NOT guaranteed to be O(1) in every possible situation.

---

# 6. Hash Collisions

Different values can produce the same bucket.

Example:

    Alice → bucket 2
    Bob   → bucket 2
    John  → bucket 2

This is a collision.

The HashSet must then distinguish between the values.

Conceptually:

    Bucket 2
       ↓
    Alice → Bob → John

If a bucket becomes heavily collided, modern Java HashMap/HashSet can use a Red-Black Tree for the bucket.

This can provide approximately:

    O(log n)

lookup within that heavily-collided bucket.

Important:

    HashSet is normally O(1) average.

Treeification is a collision-handling mechanism, not the normal way HashSet operates.

---

# 7. equals() and hashCode()

Very important Java interview concept.

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

    Alice.equals(Bob) → false

This is a hash collision.

---

# 8. Custom Objects in HashSet

Consider:

    class Person {
        String name;
    }

Then:

    Person p1 = new Person("Alice");
    Person p2 = new Person("Alice");

    Set<Person> set = new HashSet<>();

    set.add(p1);
    set.add(p2);

If Person does NOT override equals() and hashCode():

    p1.equals(p2) → false

So HashSet treats them as different objects.

Result:

    size = 2

---

## If equals() and hashCode() are overridden

Suppose equality is based on name:

    p1.equals(p2) → true

and:

    p1.hashCode() == p2.hashCode()

Then HashSet recognizes p2 as a duplicate.

Result:

    size = 1

Therefore:

> When using custom objects in HashSet, correctly implementing equals() and hashCode() is essential.

---

# 9. HashSet for Duplicate Detection

Problem:

    Given an array, determine whether it contains duplicates.

Example:

    [1, 2, 3, 4, 2]

Brute force:

    Compare every pair.

Time:

    O(n²)

Using HashSet:

    for each number:
        if it already exists:
            duplicate found
        otherwise:
            add it

Example:

    Set<Integer> set = new HashSet<>();

    for (int num : nums) {
        if (!set.add(num)) {
            return true;
        }
    }

    return false;

Important:

    HashSet.add() returns:

    true  → element was newly added
    false → element already existed

Therefore, the return value can directly tell us whether we found a duplicate.

---

# 10. Complexity of Duplicate Detection

Using HashSet:

    Time → O(n) average
    Space → O(n)

Why?

We process each element once:

    n elements

Each HashSet operation is:

    O(1) average

Therefore:

    n × O(1)
    = O(n)

The Set may store up to n unique elements:

    Space = O(n)

---

# 11. HashSet vs HashMap

## HashSet

Stores:

    value

Use when you need:

    "Have I seen this value?"

Example:

    Set<Integer> seen = new HashSet<>();

    seen.contains(x);

---

## HashMap

Stores:

    key → value

Use when you need additional information associated with the key.

Example:

    Map<Integer, Integer> map = new HashMap<>();

    number → frequency

or:

    number → index

---

# 12. Choosing Between HashSet and HashMap

Ask:

    What information do I need?

### Membership

    "Have I seen 5?"

    → HashSet

### Frequency

    "How many times have I seen 5?"

    → HashMap

### Index

    "Where did I first see 5?"

    → HashMap

### Associated data

    "What is the value associated with key 5?"

    → HashMap

The principle:

> Choose the simplest data structure that directly represents the information you need.

---

# 13. HashSet vs Array

For duplicate detection:

    Array/List:
    Search → O(n)

    HashSet:
    contains → O(1) average

Therefore:

    Brute force → O(n²)

    HashSet → O(n) average

Trade-off:

    HashSet uses additional O(n) space.

---

# 14. HashSet vs Sorted Structures

HashSet:

    Average lookup → O(1)
    Sorted order   → No

TreeSet:

    Lookup         → O(log n)
    Sorted order   → Yes

Use HashSet when:

    Fast membership is the priority.

Use TreeSet when:

    You need both uniqueness and sorted ordering.

---

# 15. Important Mental Model

Think:

                HashSet
                   |
              HashMap internally
                   |
             Array of buckets
                   |
              hashCode()
                   |
             Bucket selection
                   |
             Collision?
              /        \
            No          Yes
            |            |
          Store      Chain/tree
                         |
                      equals()
                         |
                     Duplicate?

Average operations:

    O(1)

---

# 16. Interview Questions You Should Be Able to Answer

### Why use HashSet?

> When I need fast average O(1) membership checks or uniqueness.

### Why doesn't HashSet allow duplicates?

> It uses hashing to locate the appropriate bucket and equals() to determine whether an equivalent element already exists.

### Why is HashSet O(1) average?

> Hashing allows us to locate the appropriate bucket without scanning the entire collection.

### Why isn't HashSet guaranteed O(1)?

> Hash collisions can cause multiple elements to share a bucket, increasing lookup work.

### Why are equals() and hashCode() important?

> hashCode() determines the bucket and equals() determines whether two objects are actually equal. Equal objects must have the same hash code.

### How do you detect duplicates efficiently?

> Use a HashSet and check the return value of add(). If add() returns false, the value already existed.

### Why use HashSet instead of HashMap?

> If I only need membership/uniqueness, HashSet is the simpler and more appropriate abstraction. HashMap is useful when I need additional information associated with each key.

---

# 17. HashSet vs HashMap vs Array

| Requirement | Best Choice |
|---|---|
| Fast membership | HashSet |
| Detect duplicates | HashSet |
| Value → frequency | HashMap |
| Value → index | HashMap |
| Key → associated value | HashMap |
| Fixed small set of possible values | Array |
| Sorted unique values | TreeSet |
| Sorted key → value | TreeMap |

---

# 18. One-Line Mental Model

    HashSet =
    HashMap keys
    + hashCode()
    + equals()
    + uniqueness

Average:

    add()      → O(1)
    contains() → O(1)
    remove()   → O(1)

Space:

    O(n)

# 7. TreeMap

TreeMap maintains keys in sorted order.

It is typically implemented using a balanced search tree.

### Complexity

    get()      → O(log n)
    put()      → O(log n)
    remove()   → O(log n)

### HashMap vs TreeMap

HashMap:

    Average get/put → O(1)
    Sorted order    → No

TreeMap:

    get/put         → O(log n)
    Sorted order    → Yes

### When to use TreeMap?

Use TreeMap when you need operations such as:

- Keys maintained in sorted order
- Find smallest/largest key
- Find keys within a range
- Floor/ceiling operations
- Ordered traversal

---

# 8. Stack

Stack follows:

    LIFO
    Last In, First Out

Example:

    Push A
    Push B
    Push C

    Top → C

Pop:

    C

### Typical Operations

    push() → O(1)
    pop()  → O(1)
    peek() → O(1)

### Common Uses

- DFS
- Function call stack
- Parentheses matching
- Expression evaluation
- Backtracking
- Monotonic stack problems

### Why Stack for DFS?

DFS wants to explore one path deeply before going back.

LIFO naturally provides:

    Most recently discovered node
                 ↓
             explore next

A stack can also mimic the recursive call stack used by recursive DFS.

---

# 9. Queue

Queue follows:

    FIFO
    First In, First Out

Example:

    A → B → C

Dequeue:

    A

Then:

    B → C

### Typical Operations

    enqueue/offer → O(1)
    dequeue/poll  → O(1)
    peek          → O(1)

### Common Uses

- BFS
- Task processing
- Request queues
- Producer-consumer systems
- Scheduling

### Why Queue for BFS?

BFS explores level by level.

    Level 1
      ↓
    Level 2
      ↓
    Level 3

FIFO ensures nodes discovered earlier are processed first.

---

# 10. Deque

Deque = Double Ended Queue.

It supports operations at both ends.

    Front <--------------> Back

Typical operations:

    addFirst()   → O(1)
    addLast()    → O(1)
    removeFirst() → O(1)
    removeLast()  → O(1)
    peekFirst()   → O(1)
    peekLast()    → O(1)

A deque does not have to be implemented using a doubly linked list.

For example, Java's `ArrayDeque` uses an array-based implementation.

### Common Uses

- Sliding window problems
- BFS variants
- Monotonic queue
- Implementing both stack and queue behavior

---

# 11. LRU Cache

LRU = Least Recently Used.

Suppose the cache can hold only 3 items:

    A B C

Access A:

    B C A

A is now the most recently used.

Add D:

    C A D

B is removed because it was the least recently used.

---

## Required Operations

We want:

    get(key) → O(1)
    put(key,value) → O(1)

Use two data structures:

    HashMap + Doubly Linked List

### HashMap

Stores:

    key → node

This gives:

    Find node → O(1) average

### Doubly Linked List

Maintains usage order:

    Least Recently Used <-> ... <-> Most Recently Used

Because the HashMap gives us a direct reference to the node, we can:

    Remove node → O(1)
    Move node → O(1)

Therefore:

    get() → O(1)
    put() → O(1)

### Important Interview Pattern

> HashMap provides fast lookup, while the doubly linked list provides fast ordering/reordering.

This is a classic example of combining data structures to satisfy multiple requirements.

---

# 12. Choosing the Right Data Structure

Don't memorize only complexity tables.

Instead ask:

## What operations do I need?

### Need fast membership?

    HashSet

Average:

    O(1)

---

### Need key → value lookup?

    HashMap

Average:

    O(1)

---

### Need sorted keys?

    TreeMap

    O(log n)

---

### Need fast random access?

    Array / ArrayList

    O(1)

---

### Need frequent insertion/deletion at known nodes?

    LinkedList

    O(1) once node is known

---

### Need LIFO?

    Stack / Deque

---

### Need FIFO?

    Queue / Deque

---

### Need priority-based retrieval?

    Heap / PriorityQueue

---

### Need LRU behavior?

    HashMap + Doubly Linked List

---

# 13. Interview Mindset

When choosing a data structure, think:

    1. What operations do I need?
    2. What complexity do I need for each operation?
    3. Do I need ordering?
    4. Do I need uniqueness?
    5. Do I need random access?
    6. What memory trade-off am I willing to make?

Example:

> "I need to continuously check whether I've seen a number."

Don't immediately think:

    ArrayList

Instead:

    Required operation → membership check
    Desired complexity → O(1)
    Data structure → HashSet

Example:

> "I need key-value lookup and sorted keys."

    Required → key/value + ordering
    Data structure → TreeMap

Example:

> "I need O(1) lookup and LRU eviction."

    Required → lookup + ordering
    Data structure → HashMap + Doubly Linked List



# Stack, Queue & Deque — Interview Notes

## 1. Stack

A Stack follows:

    LIFO
    Last In, First Out

Think of a stack of plates.

Example:

    push(1)
    push(2)
    push(3)

Then:

    pop() → 3
    pop() → 2
    pop() → 1

### Core operations

    push() → add element
    pop()  → remove top element
    peek() → view top element without removing

Typical complexity:

    push() → O(1) amortized
    pop()  → O(1)
    peek() → O(1)

---

# 2. Implementing a Stack

A Stack can be implemented using:

    Array / Dynamic Array
    Linked List
    Deque

## Array-based Stack

Example:

    [10][20][30]
             ↑
            top

Push:

    [10][20][30][40]
                  ↑
                 top

Pop:

    [10][20][30]
             ↑
            top

If using a dynamic array:

    push() → O(1) amortized
    pop()  → O(1)
    peek() → O(1)

Why amortized?

Occasionally the underlying array must resize, which costs O(n).

Most pushes are O(1).

---

# 3. Why use the end of an ArrayList for a Stack?

Using the end:

    [10][20][30]
             ↑
            top

push(40):

    [10][20][30][40]

No shifting is required.

Therefore:

    push → O(1) amortized
    pop  → O(1)

Using the beginning would require shifting elements.

Therefore:

    push at beginning → O(n)
    pop at beginning  → O(n)

So the end of the dynamic array is the natural choice for a Stack.

---

# 4. Stack in Java

Java has a legacy Stack class:

    Stack<Integer> stack = new Stack<>();

But generally prefer:

    Deque<Integer> stack = new ArrayDeque<>();

Example:

    Deque<Integer> stack = new ArrayDeque<>();

    stack.push(10);
    stack.push(20);

    stack.peek();
    stack.pop();

ArrayDeque is generally preferred over the legacy Stack class.

---

# 5. Queue

A Queue follows:

    FIFO
    First In, First Out

Think of a line.

Example:

    A → B → C → D

If we remove an element:

    A is removed first.

### Core operations

    offer() / add() → insert at rear
    poll() / remove() → remove from front
    peek() → inspect front

Typical complexity with a good implementation:

    enqueue → O(1)
    dequeue → O(1)
    peek    → O(1)

---

# 6. Why ArrayList is not ideal for a Queue

Suppose:

    [10][20][30][40]
     ↑
    front

If we remove 10:

    [20][30][40]

The remaining elements have to shift left.

Therefore:

    remove(0) → O(n)

This makes ArrayList a poor choice when repeatedly removing from the front.

---

# 7. LinkedList as a Queue

A LinkedList can maintain references to both ends:

    head → 10 → 20 → 30 → 40 ← tail

### Enqueue

Add to tail:

    tail → new node

Only a few pointers need to change.

    enqueue → O(1)

### Dequeue

Remove from head:

    head = head.next

Again, only a few pointer changes are required.

    dequeue → O(1)

Therefore:

    LinkedList Queue:

    enqueue → O(1)
    dequeue → O(1)
    peek    → O(1)

assuming head and tail references are maintained.

---

# 8. Deque

Deque means:

    Double Ended Queue

A Deque allows insertion and removal from BOTH ends.

Example:

    front                    rear
      ↓                       ↓
    [10] ↔ [20] ↔ [30] ↔ [40]

Operations:

    addFirst()
    addLast()

    removeFirst()
    removeLast()

    peekFirst()
    peekLast()

Typical complexity:

    addFirst()    → O(1) amortized
    addLast()     → O(1) amortized

    removeFirst() → O(1)
    removeLast()  → O(1)

    peekFirst()   → O(1)
    peekLast()    → O(1)

---

# 9. Deque can behave as both Stack and Queue

## As a Stack

Use one end:

    push()
    pop()
    peek()

This gives:

    LIFO

## As a Queue

Use different ends:

    addLast()
    removeFirst()

This gives:

    FIFO

Therefore:

    Deque
      |
      ├── Stack behavior
      |
      └── Queue behavior

This is one reason ArrayDeque is so useful.

---

# 10. ArrayDeque

In Java:

    Deque<Integer> deque = new ArrayDeque<>();

ArrayDeque can be used as:

    Stack
    Queue
    Deque

It is generally preferred over the legacy Stack class.

It is also often preferred over LinkedList when we simply need Queue/Deque behavior.

---

# 11. Why ArrayDeque is efficient

ArrayDeque uses a resizable circular array internally.

Instead of requiring the elements to always begin at index 0, the logical front and rear can move around the array.

Example:

    index:  0   1   2   3   4   5   6   7

           [D] [E] [ ] [ ] [ ] [A] [B] [C]
                              ↑       ↑
                            front   rear

The logical order is:

    A → B → C → D → E

Even though the elements are physically split across the end and beginning of the array.

---

# 12. Circular Array

A circular array treats the end of the array as connected to the beginning.

Conceptually:

              ┌───────────────┐
              ↓               ↑
          [0][1][2][3][4][5][6][7]
              ↑               ↓
              └───────────────┘

When the rear reaches the final index, it can wrap around to index 0.

Similarly, the front can wrap around.

This avoids shifting all elements when removing from the front.

---

# 13. Example of Circular Movement

Suppose:

    front = 5
    rear  = 1

and:

    index:  0   1   2   3   4   5   6   7

           [D] [E] [ ] [ ] [ ] [A] [B] [C]
                              ↑       ↑
                            front   rear

Logical order:

    A → B → C → D → E

### removeFirst()

Remove A.

Then:

    front: 5 → 6

Logical order becomes:

    B → C → D → E

### addLast(F)

The rear wraps around and F is placed at index 2.

Logical order becomes:

    B → C → D → E → F

The physical array does NOT need to contain the elements contiguously.

---

# 14. Why circular arrays are useful

Normal ArrayList removal from the beginning:

    [A][B][C][D]
     ↑

remove A

    [B][C][D]

Requires shifting:

    O(n)

Circular array:

    remove A
        ↓
    move front pointer
        ↓
    O(1)

We don't physically move all the elements.

---

# 15. ArrayDeque Complexity

Typical interview-level complexity:

    addFirst()    → O(1) amortized
    addLast()     → O(1) amortized

    removeFirst() → O(1)
    removeLast()  → O(1)

    peekFirst()   → O(1)
    peekLast()    → O(1)

Why are insertion operations amortized?

Because ArrayDeque may occasionally need to resize its underlying array.

Most operations are O(1).

Occasional resize costs O(n).

---

# 16. Stack vs Queue vs Deque

| Data Structure | Principle | Ends Used |
|---|---|---|
| Stack | LIFO | One end |
| Queue | FIFO | Add at rear, remove at front |
| Deque | Both | Both ends |

### Stack

    push → top
    pop  → top

### Queue

    add → rear
    remove → front

### Deque

    addFirst
    addLast
    removeFirst
    removeLast

---

# 17. Choosing the Data Structure

Ask:

    What operations do I need?

### Need LIFO?

    Stack

    Java:
    Deque + ArrayDeque

### Need FIFO?

    Queue

    Java:
    ArrayDeque is often a good choice

### Need both ends?

    Deque

    Java:
    ArrayDeque

### Need random access by index?

    ArrayList

### Need fast membership?

    HashSet

### Need key → value?

    HashMap

---

# 18. ArrayList vs LinkedList vs ArrayDeque

## ArrayList

Best for:

    Random access
    Index-based operations
    Appending at end

Complexities:

    get(index) → O(1)
    add(end)   → O(1) amortized
    remove(end) → O(1)
    add/remove beginning or middle → O(n)

---

## LinkedList

Best when:

    You specifically need node-based insertion/removal
    and have references to nodes / ends.

Complexities:

    get(index) → O(n)
    add/remove at ends → O(1)
    insert/remove with node reference → O(1)

However, for typical Queue/Deque usage in Java, ArrayDeque is often preferred.

---

## ArrayDeque

Best for:

    Stack
    Queue
    Deque

Complexities:

    addFirst/addLast → O(1) amortized
    removeFirst/removeLast → O(1)
    peekFirst/peekLast → O(1)

Uses:

    Resizable circular array

---

# 19. Common Interview Questions

### Why isn't ArrayList ideal for a Queue?

Removing from the beginning requires shifting the remaining elements.

    remove(0) → O(n)

### Why is ArrayList good for a Stack?

If the top is at the end:

    push → O(1) amortized
    pop  → O(1)

No shifting is required.

### Why can LinkedList implement a Queue efficiently?

It can maintain head and tail references.

    enqueue → update tail
    dequeue → update head

Both are O(1).

### Why is ArrayDeque efficient?

It uses a circular array, allowing the front and rear to move without shifting all elements.

### What is the difference between Stack and Queue?

    Stack → LIFO
    Queue → FIFO

### What is a Deque?

A Double Ended Queue where insertion and removal can occur at both ends.

### What Java structure would you use for a Stack?

    Deque<T> stack = new ArrayDeque<>();

### What Java structure would you use for a Queue?

    Queue<T> queue = new ArrayDeque<>();

### What Java structure would you use when both ends are needed?

    Deque<T> deque = new ArrayDeque<>();

---

# 20. One-Line Mental Models

Stack:

    LIFO → one end

Queue:

    FIFO → add rear, remove front

Deque:

    Both ends

ArrayList:

    Dynamic array → fast index access

LinkedList:

    Nodes + pointers → fast end/node operations

ArrayDeque:

    Circular dynamic array → efficient Stack/Queue/Deque

---

# 21. Key Interview Takeaways

1. Stack = LIFO.

2. Queue = FIFO.

3. Deque allows operations at both ends.

4. ArrayList is bad for repeated front removal because it requires shifting.

5. ArrayList is good for Stack behavior when the top is at the end.

6. LinkedList can implement a Queue in O(1) at both ends when head/tail references are maintained.

7. ArrayDeque uses a circular array.

8. ArrayDeque is generally preferred for Stack/Queue/Deque use cases in Java.

9. ArrayDeque insertion at the ends is O(1) amortized because resizing can occasionally occur.

10. Choose the data structure based on the operations the problem requires.


