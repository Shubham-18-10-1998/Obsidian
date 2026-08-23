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

