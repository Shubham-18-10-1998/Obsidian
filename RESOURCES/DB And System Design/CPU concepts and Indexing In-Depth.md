
# CPU and CPY cycle

One CPU cycle means that the CPU fetches an instruction, Decodes it and executes a part of it. Not all operations can complete in one CPU cycle.

## What happens in a CPU cycle (Simplified Pipeline)

Each instruction goes through stages:

1. **Fetch** → get instruction from memory
2. **Decode** → understand it
3. **Execute** → perform operation
4. **Write back** → store result

---

### 🔥 Important Insight

Modern CPUs use **pipelining**

👉 Multiple instructions are processed simultaneously in different stages

---

### 🍽️ Analogy

Assembly line:

- Worker 1 → fetch
- Worker 2 → decode
- Worker 3 → execute

👉 Many instructions in progress at once

# Indexing
Clustered Index : How data is stored
Non-Clustered Index : How data is found

Also index can be scanned forward or backward.

## Clustered Index
The data is stored physically in order of cluster id (sorted).
Its usually on primary key.

This is faster for range queries and lookup

Data is stored in B-Tree based on clustered key. Thus B-Tree is the table. Thus here leaf nodes contains the actual data.

This is like a dictionary, word are sorted and we directly reach the page.

### Images to help
1. ![Bot Verification](https://images.openai.com/static-rsc-4/eYAqBxkoTU4CMxxxXc3KjNZtrIepcLz-yKkmyudGmKP5yZbzR89aFvWwnml6tySr8Bz3n4SZaKd0TPkUYiou1fcVzK428PVoZGpHAJgufjZ6Sgk0vJ2AAN69rfoWR5hz42IlazXzEwp8Fp2aBW8PVDKvyTceTA9IHhalf5KiXQVaJYq5emSLw176cZSQwY2U?purpose=fullsize)
2. ![SQL Server indices. Clustered vs non-clustered indices… | by Filip Yordanov | Medium](https://images.openai.com/static-rsc-4/8Br_aHFmAbCCUgENBuA2ffiUFRhZGHKu815i4fGeKlImZJQLSciXAaXzDgzaufxfDOL3O_VH19AU4l4eSFNHkB51PpbOQgCD2mOoyH8-tQEx5qcPS3MZpx0xXHq6rffEQfbpwlSb6UZo1ckZR8lGAD7v_VSvGyy0blgqP-B31WYUwkf7e8r7VUnXjhJqlN3j?purpose=fullsize)


## Non Clustered Index
Can be many, and helps in faster lookups. This is stored in separate structure.

This is like index to reach page.
Topic -> Page number -> content

Here same B-Tree made for column but leaf node contains, column value -> pk or for heap memory its column value and RID(page and offset for row)

## Composite Structure
eg. if index on name + age ->
works on 
- name
- name + age
But **NOT** for age

Here 
- Where : First Column
- Order By : Next Columns
- 


# ❓ 2) Why do some queries ignore indexes? (🔥 interview gold)

This is asked _a lot_. The core idea:

> **Indexes are only useful when they reduce work.**

---

## 🧠 Reason 1: Low selectivity (too many rows match)

```
SELECT * FROM employees WHERE gender = 'M';
```

If 90% rows are `'M'`:

- Index → many lookups + random I/O ❌
- Full scan → sequential read ✅

👉 Optimizer chooses full scan

---

## 🧠 Reason 2: Function on column (breaks index)

```
SELECT * FROM employees WHERE UPPER(name) = 'JOHN';
```

Index is on `name`, not `UPPER(name)`  
👉 DB can’t use it (unless functional index exists)

---

## 🧠 Reason 3: Leading wildcard

```
WHERE name LIKE '%ohn'
```

B-Tree works left → right  
👉 Can’t jump into middle  
👉 Full scan

---

## 🧠 Reason 4: Small table

If table has 100 rows:  
👉 Index overhead > benefit  
👉 Full scan wins

---

## 🧠 Reason 5: Outdated statistics

Optimizer relies on stats:

- Row count
- Distribution

If stats are wrong:  
👉 Bad plan (index ignored or misused)

---

## 🧠 Reason 6: Non-covering index (double hop cost)

If query needs many columns:

```
SELECT * FROM employees WHERE salary = 120000;
```

Index gives:

```
salary → id
```

Then:

- Go to table for full row (extra I/O)

👉 Sometimes full scan is cheaper

---

## 🧠 Reason 7: Range scans returning many rows

```
WHERE salary > 10000
```

If this returns large %:  
👉 Index traversal + many lookups = expensive

---

### 🔥 Interview one-liner:

> “Indexes are ignored when the cost of using them (random I/O, lookups) exceeds a sequential scan, often due to low selectivity, functions on columns, or large result sets.”

Perfect—these two topics are exactly where your current understanding turns into real performance intuition.

---

# 🚀 Part 1: Inserts in a Clustered Index (Page Splits & Fragmentation)

You already know:

> Clustered index = data stored in sorted order (B-Tree)

Now the question is:  
👉 **What happens when new data doesn’t fit neatly?**

---

## 🔍 Example

Clustered index on `id`

Current leaf nodes:

```text
[1, 2, 3]   [5, 6, 7]
```

---

## 🟢 Case 1: Insert at the end (easy case)

```sql
INSERT INTO employees VALUES (8, ...);
```

👉 Goes to last page:

```text
[5, 6, 7, 8]
```

✔ Fast  
✔ No restructuring

---

## 🔴 Case 2: Insert in the middle (problem case)

```sql
INSERT INTO employees VALUES (4, ...);
```

👉 Should go between 3 and 5

---

### ⚠️ If page is FULL → **Page Split**

### Before:

```text
[1, 2, 3]   [5, 6, 7]
```

---

### After split:

```text
[1, 2, 3]   [4, 5]   [6, 7]
```

What happened:

- Page split into two
    
- Data redistributed
    
- Parent nodes updated
    

---

## 💥 Why page splits are bad

- Extra disk writes
    
- Tree rebalancing
    
- Slower inserts
    

---

## 💣 Fragmentation (next problem)

Over time:

```text
Logical order:   1 → 2 → 3 → 4 → 5 → 6
Physical pages:  Page9 → Page2 → Page15 → Page1
```

👉 Pages no longer contiguous on disk

---

## 🚨 Impact

- Sequential scans become slower
    
- More disk seeks
    

---

## 🧠 Analogy

Think of a bookshelf:

- Clustered index = sorted books
    
- Insert in middle → shift books
    
- No space → split shelf
    
- Over time → books scattered across room
    

---

## 💡 Practical insight (interview gold)

> “Clustered indexes on frequently changing/random columns cause page splits and fragmentation, hurting performance.”

---

## ⚡ Common solution

Use **sequential keys**:

```text
AUTO_INCREMENT / IDENTITY
```

👉 Always inserts at end → no splits

---

# 🚀 Part 2: Covering Index (Avoid the “Double Hop”)

You already know:

👉 Non-clustered index → often needs:

1. Index lookup
    
2. Table lookup
    

---

## 🔍 Example

```sql
SELECT name 
FROM employees 
WHERE salary = 120000;
```

---

## Without covering index

Index:

```text
salary → id
```

Flow:

1. Find salary
    
2. Get `id`
    
3. Go to clustered index
    
4. Fetch `name`
    

👉 ❌ Double hop

---

## ✅ Covering index

```sql
CREATE INDEX idx_salary ON employees(salary, name);
```

---

### Now index contains:

```text
salary → name
```

---

## 🚀 Execution now:

1. Search index
    
2. Get `name` directly
    

👉 No table lookup  
👉 No double hop

---

## 🔥 Why it's powerful

- Fewer I/O operations
    
- Faster queries
    
- Index alone satisfies query
    

---

## 🧠 Analogy

### Without covering index:

> Index says: “Go to page 42 for name”

### With covering index:

> Index says: “Here’s the name directly”

---

# ⚠️ Trade-offs

Covering indexes are not free:

### ❌ Cons:

- More storage
    
- Slower inserts/updates
    
- More maintenance
    

---

# 🧠 When to use

Best when:

- Query runs frequently
    
- Reads >> Writes
    
- Few columns needed
    

---

# 🔥 Interview-ready summary

### Page Splits

> Occur when inserting into a full page in a clustered index, causing page division and potential fragmentation.

---

### Fragmentation

> Logical order differs from physical order, slowing scans.

---

### Covering Index

> An index that contains all columns required by a query, eliminating the need to access the base table.

---

# 💡 Final connection (everything tied together)

When a query runs:

- Optimizer checks:
    
    - Can I use index?
        
    - Is it covering?
        
- If yes:
    
    - Avoid double hop
        
- If clustered:
    
    - Inserts may cause splits
        
- If fragmented:
    
    - Scans slower
        

---

Great—these two tie everything you’ve learned into something you can _see_ and reason about.

---

# 🚀 Part 1: Execution Plans (`EXPLAIN`)

Think of an execution plan as:

> **“The exact step-by-step strategy the database will use to run your query.”**

---

## 🔍 Example Query

```sql
SELECT name 
FROM employees 
WHERE salary = 120000;
```

---

## 🧠 What the optimizer decides

It might choose:

- Index scan?
    
- Full table scan?
    
- Covering index?
    

---

## 📄 Example Execution Plan (simplified)

```text
Index Seek (idx_salary)
  → Key Lookup (Clustered Index)
    → Output: name
```

---

## 🧩 Breaking this down

### 1. **Index Seek**

- Use B-Tree on `salary`
    
- Find matching entries fast
    

👉 This is your **index traversal**

---

### 2. **Key Lookup (important)**

- Use `id` from index
    
- Go to clustered index
    
- Fetch full row
    

👉 This is your **double hop**

---

### 3. **Output**

- Return `name`
    

---

## 🔥 If covering index exists

```sql
CREATE INDEX idx_salary ON employees(salary, name);
```

---

### Plan becomes:

```text
Index Seek (idx_salary)
  → Output: name
```

👉 No key lookup  
👉 Faster

---

## 🧠 Key operators you should know (interview must-know)

|Operator|Meaning|
|---|---|
|**Seq Scan / Table Scan**|Full table read|
|**Index Seek**|Efficient lookup using index|
|**Index Scan**|Scan part of index|
|**Key Lookup**|Fetch row from table using PK|
|**Filter**|Apply condition|
|**Nested Loop Join**|Loop-based join|
|**Hash Join**|Hash-based join|

---

## ⚡ Quick intuition

- **Seek** → fast, targeted
    
- **Scan** → broad, expensive
    
- **Key Lookup** → extra cost (avoid if possible)
    

---

## 🧠 Analogy

Execution plan = GPS route

- Index Seek → highway
    
- Table Scan → walking every street
    
- Key Lookup → detour to pick something up
    

---

# 🚀 Part 2: Join Algorithms (Core DB engine behavior)

When you do:

```sql
SELECT e.name, d.name
FROM employees e
JOIN departments d 
ON e.department_id = d.id;
```

👉 Database must decide:

> “How do I combine these two tables efficiently?”

---

# 🔵 1. Nested Loop Join

---

## 🧠 How it works

```text
for each row in employees:
    find matching row in departments
```

---

## 🔍 Example

```text
Employees:   100 rows  
Departments: 10 rows
```

---

## ⚡ Best case

- Small outer table
    
- Index on inner table
    

👉 Very fast

---

## ❌ Worst case

- Large tables
    
- No index
    

👉 Very slow (O(n²))

---

## 🧠 Analogy

> For each person, search entire phonebook

---

# 🟢 2. Hash Join

---

## 🧠 How it works

### Step 1: Build hash table

```text
Hash departments on id
```

### Step 2: Probe

```text
For each employee:
    check hash for match
```

---

## ⚡ Performance

- O(n)
    
- Very efficient for large datasets
    

---

## ❌ Downsides

- Needs memory
    
- Hash build cost
    

---

## 🧠 Analogy

> Build a dictionary → lookup instantly

---

# 🟣 3. Merge Join

---

## 🧠 Requirement

Both tables must be **sorted on join key**

---

## 🔍 How it works

```text
Compare rows in order:
Move pointers forward like merge step in merge sort
```

---

## ⚡ Performance

- Very fast for sorted data
    
- No hashing needed
    

---

## 🧠 Analogy

> Two sorted lists → walk through together

---

# ⚖️ When does DB choose which?

|Situation|Join chosen|
|---|---|
|Small + indexed|Nested Loop|
|Large, unsorted|Hash Join|
|Already sorted|Merge Join|

---

# 🔥 Connecting EVERYTHING you learned

Let’s combine:

---

## Query

```sql
SELECT e.name
FROM employees e
JOIN departments d 
ON e.department_id = d.id
WHERE d.name = 'Engineering';
```

---

## Possible execution plan

```text
Index Seek (departments.name = 'Engineering')
  → Hash Join
      → Seq Scan (employees)
      → Hash (departments)
```

---

## What’s happening

1. Filter departments
    
2. Build hash
    
3. Scan employees
    
4. Match via hash
    
5. Return names
    

---

# 💡 Interview-level insights

### 🔥 Why Nested Loop can be fast

> If inner table has index → lookup is O(log n)

---

### 🔥 Why Hash Join is preferred

> For large joins without indexes

---

### 🔥 Why Merge Join is rare but powerful

> When data already sorted (e.g., clustered index)

---

# 🚀 Final Mental Model

When a query runs:

1. Parse + Rewrite
    
2. Optimizer decides:
    
    - Index or scan?
        
    - Join type?
        
3. Execution plan created
    
4. Engine executes operators:
    
    - Seek, Scan, Join
        

---

