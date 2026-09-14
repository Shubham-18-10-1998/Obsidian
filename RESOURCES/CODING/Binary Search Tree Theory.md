
# Binary Search Tree (BST)

## 1. What is a BST?

A Binary Search Tree is a Binary Tree with an ordering property.

For every node:

```text
All values in LEFT subtree  < node
All values in RIGHT subtree > node
```

Example:

```text
        8
       / \
      3   10
     / \    \
    1   6    14
       / \   /
      4   7 13
```

Important:

The rule applies to the ENTIRE subtree, not just the immediate children.

---

# 2. BST vs Binary Tree vs Heap

## Binary Tree

Each node can have at most 2 children.

There is no ordering requirement.

## Binary Search Tree

Binary Tree +

```text
left subtree < node < right subtree
```

## Heap

Complete Binary Tree +

For Min Heap:

```text
parent <= children
```

For Max Heap:

```text
parent >= children
```

A Heap does NOT have the BST ordering property.

---

# 3. Inorder Traversal of a BST

Inorder traversal:

```text
LEFT -> ROOT -> RIGHT
```

For a valid BST, inorder traversal produces values in sorted order.

Example:

```text
        5
       / \
      3   8
     / \   \
    1   4   10
```

Inorder:

```text
1 -> 3 -> 4 -> 5 -> 8 -> 10
```

This is an important BST property for interview problems.

---

# 4. BST Search

At every node:

```text
target == node
    -> Found

target < node
    -> Search LEFT

target > node
    -> Search RIGHT
```

Example: Search for 13

```text
        8
         \
         10
           \
           14
          /
         13
```

Path:

```text
13 > 8
-> RIGHT

13 > 10
-> RIGHT

13 < 14
-> LEFT

13 == 13
-> FOUND
```

## Why is BST search efficient?

At each node, the BST property allows us to completely ignore one subtree.

We therefore only travel along one path from the root.

## Complexity

Let `h` = height of tree.

```text
Time = O(h)
```

Balanced BST:

```text
h = O(log n)

Search = O(log n)
```

Completely skewed BST:

```text
h = O(n)

Search = O(n)
```

Iterative search:

```text
Auxiliary Space = O(1)
```

Recursive search:

```text
Auxiliary Space = O(h)
```

because of the recursion stack.

---

# 5. BST Insertion

Insertion uses almost the same logic as search.

Starting from the root:

```text
value < current
    -> go LEFT

value > current
    -> go RIGHT
```

Continue until the required child is `null`.

Insert the new node there.

Example: Insert 5

```text
        8
       /
      3
       \
        6
       /
      4
```

Decisions:

```text
5 < 8
-> LEFT

5 > 3
-> RIGHT

5 < 6
-> LEFT

5 > 4
-> RIGHT
```

`4.right` is null.

Therefore:

```text
4.right = 5
```

Result:

```text
        8
       /
      3
       \
        6
       /
      4
       \
        5
```

## Why does this preserve the BST?

We make every decision using the BST ordering property.

When we finally reach `null`, we know that this is the correct position for the value.

## Complexity

```text
Time = O(h)
```

Balanced:

```text
O(log n)
```

Skewed:

```text
O(n)
```

Iterative auxiliary space:

```text
O(1)
```

---

# 6. BST Deletion

Deletion is more complicated because removing a node must not break the BST property.

There are 3 cases.

---

## Case 1: Node has no children

Example:

```text
    3
   /
  1
```

Delete `1`:

```text
    3
   /
 null
```

Simply remove the node.

---

## Case 2: Node has one child

Example:

```text
    3
   /
  1
   \
    2
```

Delete `1`.

Connect its parent directly to its child:

```text
    3
   /
  2
```

General idea:

```text
Deleted node has only LEFT child
-> replace node with LEFT child

Deleted node has only RIGHT child
-> replace node with RIGHT child
```

---

## Case 3: Node has two children

This is the interesting case.

Example:

```text
          6
        /   \
       4     10
      / \    / \
     2   5  8   12
```

We cannot simply remove `6`, because we need to preserve both subtrees.

One solution:

Find the SMALLEST value in the RIGHT subtree.

For the example:

```text
Right subtree:

       10
      /  \
     8    12
```

Smallest value = `8`

Replace:

```text
6 -> 8
```

Then remove the ORIGINAL `8` from the right subtree.

Result:

```text
          8
        /   \
       4     10
      / \      \
     2   5      12
```

---

# 7. Why Does the Smallest Value in the Right Subtree Work?

Suppose we're deleting:

```text
       X
      / \
   LEFT RIGHT
```

The smallest value in `RIGHT` is:

```text
> everything in LEFT
```

and is also:

```text
<= everything else in RIGHT
```

Therefore it can safely replace `X`.

This value is commonly called the:

```text
Inorder Successor
```

---

# 8. Important Property of the Smallest Node

To find the smallest node in a BST/subtree:

```text
Keep going LEFT until:

node.left == null
```

Therefore, the smallest node CANNOT have a left child.

It MAY have a right child.

Example:

```text
       10
      /
     8
      \
       9
```

`8` is the smallest node, but it has a right child.

Therefore when removing the original successor, we must preserve its right child if one exists.

---

# 9. Alternative for Deletion

Instead of:

```text
Smallest value in RIGHT subtree
```

we can also use:

```text
Largest value in LEFT subtree
```

This is commonly called the:

```text
Inorder Predecessor
```

So for a node with two children:

```text
Option 1:
Smallest in RIGHT subtree
= Inorder Successor

Option 2:
Largest in LEFT subtree
= Inorder Predecessor
```

Either can be used while preserving the BST.

---

# 10. BST Operation Complexity Summary

Let:

```text
h = height of tree
```

| Operation | Balanced BST | Skewed BST |
|---|---:|---:|
| Search | O(log n) | O(n) |
| Insert | O(log n) | O(n) |
| Delete | O(log n) | O(n) |
| Find Min | O(log n) | O(n) |
| Find Max | O(log n) | O(n) |

More generally:

```text
Search = O(h)
Insert = O(h)
Delete = O(h)
```

The complexity depends on TREE HEIGHT.

---

# 11. Why Can a BST Become O(n)?

A normal BST does NOT guarantee that it stays balanced.

For example, inserting:

```text
1, 2, 3, 4, 5
```

could produce:

```text
1
 \
  2
   \
    3
     \
      4
       \
        5
```

This behaves almost like a linked list.

Height:

```text
h = n
```

Therefore:

```text
Search = O(n)
Insert = O(n)
Delete = O(n)
```

This is why balanced BST implementations exist.

Examples:

```text
AVL Tree
Red-Black Tree
```

Java's `TreeMap` and `TreeSet` use a Red-Black Tree.

Therefore their important operations are generally:

```text
O(log n)
```

---

# 12. Important Interview Mental Models

## Search

```text
Compare
   ↓
Go LEFT or RIGHT
   ↓
Ignore the other subtree
```

## Insert

```text
Search for where the value SHOULD be
   ↓
Reach null
   ↓
Insert there
```

## Delete

```text
Find node
   ↓
How many children?

0 children
-> remove

1 child
-> replace with child

2 children
-> find successor/predecessor
-> replace value
-> remove original replacement node
```

---

# Key Takeaways

```text
BST PROPERTY:

LEFT < ROOT < RIGHT
```

This applies recursively to every subtree.

Because of this property:

```text
Search / Insert / Delete
        ↓
Only need to follow one path
        ↓
O(height)
```

Balanced:

```text
O(log n)
```

Skewed:

```text
O(n)
```

And remember:

```text
Inorder traversal of BST
        ↓
Sorted order
```