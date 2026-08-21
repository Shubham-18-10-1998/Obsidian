
There are three types of time complexities
- Worst Case (Big O)
- Best Case (Big Omega)
- Average Case (Big Theta)


# Big O Notation (Worst Case Scenario)
It means the function cant grow faster than this, hence worst case scenario. This is in terms of mathematics, and hence we use this to denote the worst case time complexity.

# Big Omega Notation (Best Case Scenario)
It means the function at least grows at this pace in mathematics. Hence used to show the best case time complexity.

# Big Theta Notation (Average Case Scenario)
It means this is the asymptotic growth rate of the function. Hence shows the average rate for the function.

# Learning Examples

## Hash-Map
Here lookup is O(1) on average as the keys are usually evenly distributed and thus there are a constant number of comparisons. Hence the average time complexity is O(1). However, if there are collisions, that is many keys collide in the same bucket, then worst case time complexity is O(N). However Java Treeify sufficiently large collisions making the complexity O(log(N)).

# Calculating Time Complexity
Working method is, try to see range of i or the outer loops and how much iterations are the for that value in the inside loops. And then summarise them (the effort) in total, and thats the worst case time complexity.


# Master Theorem

Used to solve recurrence relations of the form:

$$
T(n) = aT\left(\frac{n}{b}\right) + f(n)
$$

Where:

- `a` = number of recursive subproblems
- `b` = factor by which the input size is reduced
- `f(n)` = work done outside the recursive calls

---

## Step 1: Calculate the critical term

Calculate:

$$
n^{\log_b a}
$$

Then compare `f(n)` with:

$$
n^{\log_b a}
$$

---

## Case 1: Recursive work dominates

If:

$$
f(n) = O\left(n^{\log_b a - \epsilon}\right)
$$

for some constant $\epsilon > 0$, then:

$$
T(n) = \Theta\left(n^{\log_b a}\right)
$$

### Example

$$
T(n) = 2T(n/2) + 1
$$

Here:

$$
a = 2,\quad b = 2
$$

Therefore:

$$
n^{\log_2 2} = n
$$

Since:

$$
f(n) = 1
$$

is smaller than `n`:

$$
T(n) = \Theta(n)
$$

---

## Case 2: Recursive work and outside work are balanced

If:

$$
f(n) = \Theta\left(n^{\log_b a}\log^k n\right)
$$

then:

$$
T(n) = \Theta\left(n^{\log_b a}\log^{k+1}n\right)
$$

The most common case is:

$$
f(n) = \Theta\left(n^{\log_b a}\right)
$$

Then:

$$
T(n) = \Theta\left(n^{\log_b a}\log n\right)
$$

### Example: Merge Sort

$$
T(n) = 2T(n/2) + n
$$

Here:

$$
a = 2,\quad b = 2
$$

So:

$$
n^{\log_2 2} = n
$$

And:

$$
f(n) = n
$$

Therefore this is Case 2:

$$
T(n) = \Theta(n\log n)
$$

---

## Case 3: Outside work dominates

If:

$$
f(n) = \Omega\left(n^{\log_b a + \epsilon}\right)
$$

for some constant $\epsilon > 0$, and the regularity condition is satisfied, then:

$$
T(n) = \Theta(f(n))
$$

### Example

$$
T(n) = 2T(n/2) + n^2
$$

Here:

$$
n^{\log_2 2} = n
$$

But:

$$
f(n) = n^2
$$

Since $n^2$ grows faster than $n$:

$$
T(n) = \Theta(n^2)
$$

---

# Quick Way to Remember

First calculate:

$$
C = n^{\log_b a}
$$

Then compare `f(n)` with `C`:

| Comparison | Case | Result |
|---|---|---|
| `f(n)` is polynomially smaller than `C` | Case 1 | $\Theta(C)$ |
| `f(n)` is same order as `C` | Case 2 | $\Theta(C\log n)$ |
| `f(n)` is polynomially larger than `C` | Case 3 | $\Theta(f(n))$ |

### Mental Model

- **Case 1:** Recursive calls dominate
- **Case 2:** Recursive work and outside work are balanced
- **Case 3:** Outside work dominates

---

# Important Limitation

Master Theorem only directly applies to recurrences of the form:

$$
T(n) = aT(n/b) + f(n)
$$

The recursive subproblems must have the same size.

For example:

$$
T(n) = T(n/2) + T(n/4) + n
$$

does **not** directly fit the Master Theorem because the recursive calls have different input sizes.

For such recurrences, use:

- Recursion tree
- Substitution method
- Recurrence-tree analysis
- Other recurrence techniques

## Master Theorem Cheat Sheet
T(n) = aT(n/b) + f(n)

1. Calculate C = n^(log_b a)

2. Compare f(n) vs C

f(n) smaller → Case 1 → C
f(n) same    → Case 2 → C log n
f(n) bigger  → Case 3 → f(n)


