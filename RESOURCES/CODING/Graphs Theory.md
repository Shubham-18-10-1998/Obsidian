
# 1. What Is a Graph?

A graph is a data structure used to represent relationships between objects.

A graph consists of:

- **Vertices (Nodes):** Objects or entities.
- **Edges:** Connections or relationships between vertices.

Examples:

- Cities connected by roads.
- People connected through friendships.
- Web pages connected by hyperlinks.
- Computers connected through a network.
- Courses connected through prerequisites.

## Basic Terminology

- **Vertex / Node:** A point in the graph.
- **Edge:** A connection between two vertices.
- **Degree:** Number of edges connected to a vertex in an undirected graph.
- **Indegree:** Number of incoming edges in a directed graph.
- **Outdegree:** Number of outgoing edges in a directed graph.
- **Path:** A sequence of vertices connected by edges.
- **Cycle:** A path that starts and ends at the same vertex.
- **Connected Graph:** Every vertex is reachable from every other vertex, directly or indirectly.
- **Component:** A maximal connected subgraph.
- **Weight:** A value associated with an edge, such as cost or distance.
- **Distance:** Cost or number of edges between two vertices.

---

# 2. Types of Graphs

## 2.1 Undirected Graph

Edges have no direction.

If there is an edge between `A` and `B`, then movement is possible in both directions.

Example:

    A --- B
    |     |
    C --- D

The edge `(A, B)` is equivalent to `(B, A)`.

Common examples:

- Friendships
- Roads where traffic moves in both directions
- Network connections

## 2.2 Directed Graph

Edges have a direction.

Example:

    A → B → C

The edge `A → B` does not imply `B → A`.

Common examples:

- Prerequisite relationships
- Following relationships on social media
- One-way roads

## 2.3 Weighted Graph

Each edge has a weight.

Example:

    A --5-- B --2-- C

The weight may represent:

- Distance
- Travel time
- Cost
- Risk
- Network latency

## 2.4 Unweighted Graph

All edges are considered to have equal cost.

Example:

    A --- B --- C

For shortest-path problems in unweighted graphs, BFS is usually the correct algorithm.

## 2.5 Cyclic Graph

Contains at least one cycle.

Example:

    A → B → C → A

## 2.6 Acyclic Graph

Contains no cycles.

A directed acyclic graph is called a **DAG**.

Examples:

- Course prerequisites
- Build dependencies
- Task scheduling

## 2.7 Connected Graph

An undirected graph is connected if every node can reach every other node.

## 2.8 Disconnected Graph

A graph is disconnected if it contains multiple connected components.

Example:

    A --- B       C --- D

There are two connected components.

## 2.9 Complete Graph

Every pair of distinct vertices has an edge between them.

For `n` vertices in an undirected complete graph:

    Number of edges = n * (n - 1) / 2

---

# 3. How to Represent a Graph

There are three common representations:

1. Edge List
2. Adjacency Matrix
3. Adjacency List

---

# 4. Edge List

Store every edge as a pair.

Example graph:

    0 --- 1
    |     |
    2 --- 3

Edges:

    [[0, 1], [0, 2], [1, 3], [2, 3]]

For weighted graphs:

    [[0, 1, 5], [1, 3, 2]]

Here:

- `0` and `1` are vertices.
- `5` is the edge weight.

## Advantages

- Simple representation.
- Useful when processing all edges.
- Useful in algorithms such as Kruskal's Minimum Spanning Tree.

## Disadvantages

- Finding all neighbors of a node requires scanning all edges.
- Not efficient for BFS or DFS.

---

# 5. Adjacency Matrix

Use a 2D matrix.

If there is an edge between two vertices, store `1` or the edge weight.

Example:

    0 --- 1
    |     |
    2 --- 3

Adjacency matrix:

    [
      [0, 1, 1, 0],
      [1, 0, 0, 1],
      [1, 0, 0, 1],
      [0, 1, 1, 0]
    ]

For a weighted graph, store the weight instead of `1`.

## Advantages

- Checking whether an edge exists takes `O(1)`.
- Useful for dense graphs.
- Simple implementation.

## Disadvantages

- Requires `O(V²)` space.
- Iterating through neighbors takes `O(V)`.
- Wasteful for sparse graphs.

---

# 6. Adjacency List

Store a list of neighbors for every vertex.

Example:

    0 --- 1
    |     |
    2 --- 3

Adjacency list:

    0 → [1, 2]
    1 → [0, 3]
    2 → [0, 3]
    3 → [1, 2]

In Java:

    List<List<Integer>> graph = new ArrayList<>();

    for (int i = 0; i < n; i++) {
        graph.add(new ArrayList<>());
    }

    graph.get(0).add(1);
    graph.get(1).add(0);

For a weighted graph:

    class Edge {
        int to;
        int weight;

        Edge(int to, int weight) {
            this.to = to;
            this.weight = weight;
        }
    }

## Advantages

- Space efficient for sparse graphs.
- Efficiently iterates over neighbors.
- Most common representation in interview problems.

## Disadvantages

- Checking whether a specific edge exists may take `O(degree)`.

---

# 7. Adjacency List Complexity

For a graph with:

- `V` = number of vertices
- `E` = number of edges

### Undirected Graph

Each edge appears twice in the adjacency list.

    Space = O(V + E)

### Directed Graph

Each edge appears once.

    Space = O(V + E)

### Adjacency Matrix

    Space = O(V²)

---

# 8. Building an Undirected Graph

Suppose the input is:

    edges = [[0, 1], [0, 2], [1, 3]]

For every edge `(u, v)`:

- Add `v` to `u`'s neighbors.
- Add `u` to `v`'s neighbors.

Java:

    List<List<Integer>> graph = new ArrayList<>();

    for (int i = 0; i < n; i++) {
        graph.add(new ArrayList<>());
    }

    for (int[] edge : edges) {
        int u = edge[0];
        int v = edge[1];

        graph.get(u).add(v);
        graph.get(v).add(u);
    }

---

# 9. Building a Directed Graph

For a directed edge `u → v`:

- Add `v` to `u`'s adjacency list.
- Do not add `u` to `v`.

Java:

    for (int[] edge : edges) {
        int u = edge[0];
        int v = edge[1];

        graph.get(u).add(v);
    }

---

# 10. Graph Traversal

Graph traversal means visiting nodes systematically.

The two fundamental traversal algorithms are:

1. Breadth-First Search (BFS)
2. Depth-First Search (DFS)

Both generally take:

    Time: O(V + E)
    Space: O(V)

This assumes an adjacency-list representation.

---

# 11. Breadth-First Search (BFS)

BFS explores a graph level by level.

It uses a queue.

Example:

    A
   / \
  B   C
 / \
D   E

BFS order:

    A → B → C → D → E

## BFS Idea

1. Start from a source node.
2. Add it to a queue.
3. Mark it visited.
4. Remove a node from the queue.
5. Visit all unvisited neighbors.
6. Add those neighbors to the queue.
7. Repeat until the queue is empty.

## BFS Java Template

    Queue<Integer> queue = new LinkedList<>();
    boolean[] visited = new boolean[n];

    queue.offer(start);
    visited[start] = true;

    while (!queue.isEmpty()) {
        int node = queue.poll();

        for (int neighbor : graph.get(node)) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                queue.offer(neighbor);
            }
        }
    }

---

# 12. Why Mark Visited When Adding to the Queue?

Mark nodes visited when enqueuing them, not when removing them.

Correct:

    if (!visited[neighbor]) {
        visited[neighbor] = true;
        queue.offer(neighbor);
    }

If you mark them only when dequeuing, multiple parents may enqueue the same node.

This causes unnecessary work and can lead to incorrect behavior in some implementations.

---

# 13. BFS with Distance / Levels

BFS is especially useful for shortest paths in unweighted graphs.

Every edge has equal cost, so the first time BFS reaches a node, it has found the shortest number of edges from the source.

Example:

    A
   / \
  B   C
   \ /
    D

Distances from `A`:

- `A = 0`
- `B = 1`
- `C = 1`
- `D = 2`

Java:

    Queue<Integer> queue = new LinkedList<>();
    int[] distance = new int[n];

    Arrays.fill(distance, -1);

    distance[start] = 0;
    queue.offer(start);

    while (!queue.isEmpty()) {
        int node = queue.poll();

        for (int neighbor : graph.get(node)) {
            if (distance[neighbor] == -1) {
                distance[neighbor] = distance[node] + 1;
                queue.offer(neighbor);
            }
        }
    }

---

# 14. BFS Level-by-Level Template

Useful for problems involving:

- Number of levels
- Minimum moves
- Multi-source spreading
- Rotting oranges
- Word ladder
- Binary tree levels

Java:

    Queue<Integer> queue = new LinkedList<>();
    boolean[] visited = new boolean[n];

    queue.offer(start);
    visited[start] = true;

    int level = 0;

    while (!queue.isEmpty()) {
        int size = queue.size();

        for (int i = 0; i < size; i++) {
            int node = queue.poll();

            for (int neighbor : graph.get(node)) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.offer(neighbor);
                }
            }
        }

        level++;
    }

---

# 15. Multi-Source BFS

Sometimes there are multiple starting nodes.

Examples:

- Rotting oranges
- Distance from nearest zero
- Walls and gates
- Fire spreading
- Infection spreading

Instead of starting with one source, add all sources to the queue initially.

Java pattern:

    Queue<Integer> queue = new LinkedList<>();

    for (int i = 0; i < n; i++) {
        if (isSource(i)) {
            queue.offer(i);
            visited[i] = true;
        }
    }

    while (!queue.isEmpty()) {
        int node = queue.poll();

        for (int neighbor : graph.get(node)) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                queue.offer(neighbor);
            }
        }
    }

All sources begin at distance `0`.

---

# 16. Depth-First Search (DFS)

DFS explores as deeply as possible before backtracking.

It can be implemented using:

- Recursion
- Explicit Stack

Example:

    A
   / \
  B   C
 / \
D   E

One possible DFS order:

    A → B → D → E → C

The exact order depends on adjacency-list ordering.

---

# 17. Recursive DFS Java Template

    void dfs(int node,
             List<List<Integer>> graph,
             boolean[] visited) {

        visited[node] = true;

        for (int neighbor : graph.get(node)) {
            if (!visited[neighbor]) {
                dfs(neighbor, graph, visited);
            }
        }
    }

Call it with:

    dfs(start, graph, visited);

---

# 18. Iterative DFS Java Template

    Stack<Integer> stack = new Stack<>();
    boolean[] visited = new boolean[n];

    stack.push(start);

    while (!stack.isEmpty()) {
        int node = stack.pop();

        if (visited[node]) {
            continue;
        }

        visited[node] = true;

        for (int neighbor : graph.get(node)) {
            if (!visited[neighbor]) {
                stack.push(neighbor);
            }
        }
    }

Using `ArrayDeque` is generally preferred over the legacy `Stack` class:

    Deque<Integer> stack = new ArrayDeque<>();

    stack.push(start);

    while (!stack.isEmpty()) {
        int node = stack.pop();
    }

---

# 19. BFS vs DFS

| Feature | BFS | DFS |
|---|---|---|
| Main data structure | Queue | Stack / Recursion |
| Exploration | Level by level | Depth first |
| Shortest path in unweighted graph | Yes | No |
| Cycle detection | Yes | Yes |
| Connected components | Yes | Yes |
| Topological sorting | Kahn's algorithm | DFS ordering |
| Maze exploration | Possible | Common |
| Space complexity | O(V) | O(V) |

---

# 20. When to Use BFS

Use BFS when the problem asks for:

- Minimum number of moves.
- Shortest path in an unweighted graph.
- Nearest node.
- Minimum transformations.
- Level-by-level processing.
- Spread over time.
- Minimum number of edges.

Typical keywords:

- Shortest
- Minimum steps
- Fewest moves
- Nearest
- Distance
- Levels

---

# 21. When to Use DFS

Use DFS when the problem asks for:

- Explore all possibilities.
- Connected components.
- Detect cycles.
- Count islands.
- Backtracking through a graph.
- Path existence.
- Topological sorting.
- Recursive dependency exploration.

Typical keywords:

- Connected
- Reachable
- Explore
- Component
- Cycle
- Dependency

---

# 22. Visited Array

The visited array prevents repeatedly processing the same node.

For a graph with `n` vertices:

    boolean[] visited = new boolean[n];

Initially:

    false false false false

After visiting nodes `0` and `2`:

    true false true false

Without visited tracking:

- Cyclic graphs can cause infinite loops.
- Nodes may be processed repeatedly.
- Time complexity may become much worse.

---

# 23. Handling Disconnected Graphs

Starting DFS or BFS from one node only explores its connected component.

To visit every node:

    boolean[] visited = new boolean[n];

    for (int i = 0; i < n; i++) {
        if (!visited[i]) {
            dfs(i, graph, visited);
        }
    }

This pattern is extremely important.

It is used for:

- Counting connected components.
- Number of provinces.
- Number of islands.
- Detecting cycles across the entire graph.
- Checking whether every node belongs to some component.

---

# 24. Number of Connected Components

Given an undirected graph, count how many disconnected groups exist.

## Approach

1. Build the adjacency list.
2. Maintain a visited array.
3. Iterate through every vertex.
4. If a vertex is unvisited, start DFS/BFS.
5. Increment the component count.

Java:

    int countComponents(int n, int[][] edges) {
        List<List<Integer>> graph = new ArrayList<>();

        for (int i = 0; i < n; i++) {
            graph.add(new ArrayList<>());
        }

        for (int[] edge : edges) {
            int u = edge[0];
            int v = edge[1];

            graph.get(u).add(v);
            graph.get(v).add(u);
        }

        boolean[] visited = new boolean[n];
        int components = 0;

        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                components++;
                dfs(i, graph, visited);
            }
        }

        return components;
    }

---

# 25. Connected Components in a Grid

A grid can be treated as a graph.

Each cell is a node.

Adjacent cells are connected according to the allowed directions.

For a standard four-directional grid:

    int[][] directions = {
        {-1, 0},
        {1, 0},
        {0, -1},
        {0, 1}
    };

For eight directions:

    int[][] directions = {
        {-1, -1}, {-1, 0}, {-1, 1},
        {0, -1},           {0, 1},
        {1, -1},  {1, 0},  {1, 1}
    };

---

# 26. Number of Islands

A classic grid traversal problem.

Given a grid containing land and water, count connected groups of land.

## DFS Idea

1. Iterate through every cell.
2. When land is found, increment the island count.
3. Run DFS from that cell.
4. Mark all connected land as visited.
5. Continue scanning.

Java:

    void dfs(char[][] grid, int r, int c) {
        int rows = grid.length;
        int cols = grid[0].length;

        if (r < 0 || r >= rows ||
            c < 0 || c >= cols ||
            grid[r][c] != '1') {
            return;
        }

        grid[r][c] = '0';

        dfs(grid, r + 1, c);
        dfs(grid, r - 1, c);
        dfs(grid, r, c + 1);
        dfs(grid, r, c - 1);
    }

Time complexity:

    O(rows * cols)

Space complexity:

    O(rows * cols) in the worst case because of recursion depth.

---

# 27. Grid Traversal Template

For most grid problems, use this structure:

    for (int r = 0; r < rows; r++) {
        for (int c = 0; c < cols; c++) {

            if (condition(grid[r][c])) {
                dfs(grid, r, c);
            }
        }
    }

DFS boundary check:

    if (r < 0 || r >= rows ||
        c < 0 || c >= cols) {
        return;
    }

Always ask:

- What counts as a neighbor?
- What cells are valid?
- How do I mark a visited cell?
- Is diagonal movement allowed?

---

# 28. Cycle Detection in an Undirected Graph

An undirected graph contains a cycle if DFS encounters a visited neighbor that is not the node from which it arrived.

Why?

If you are at `B`, and `B` sees a visited node `A`, that may simply be the parent edge.

Therefore, track the parent.

Example:

    A --- B
     \   /
       C

There is a cycle.

## DFS Logic

For each neighbor:

1. If unvisited, recurse.
2. If visited and neighbor is not the parent, a cycle exists.

Java:

    boolean hasCycle(int node,
                     int parent,
                     List<List<Integer>> graph,
                     boolean[] visited) {

        visited[node] = true;

        for (int neighbor : graph.get(node)) {
            if (!visited[neighbor]) {
                if (hasCycle(neighbor, node, graph, visited)) {
                    return true;
                }
            } else if (neighbor != parent) {
                return true;
            }
        }

        return false;
    }

For a disconnected graph:

    for (int i = 0; i < n; i++) {
        if (!visited[i]) {
            if (hasCycle(i, -1, graph, visited)) {
                return true;
            }
        }
    }

---

# 29. Cycle Detection in an Undirected Graph Using BFS

Instead of recursion, store both:

- Current node.
- Parent node.

Java:

    Queue<int[]> queue = new LinkedList<>();

    queue.offer(new int[]{start, -1});
    visited[start] = true;

    while (!queue.isEmpty()) {
        int[] current = queue.poll();

        int node = current[0];
        int parent = current[1];

        for (int neighbor : graph.get(node)) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                queue.offer(new int[]{neighbor, node});
            } else if (neighbor != parent) {
                return true;
            }
        }
    }

---

# 30. Cycle Detection in a Directed Graph

The parent concept from undirected graphs does not work directly for directed graphs.

Use DFS recursion state.

There are three states:

- `0` = Unvisited
- `1` = Visiting / Currently in recursion stack
- `2` = Fully processed

A cycle exists when DFS reaches a node with state `1`.

## Example

    A → B → C
        ↑   ↓
        └───┘

When processing `C`, reaching `B` again means `B` is still in the current recursion path.

Therefore, there is a cycle.

Java:

    boolean dfs(int node,
                List<List<Integer>> graph,
                int[] state) {

        if (state[node] == 1) {
            return true;
        }

        if (state[node] == 2) {
            return false;
        }

        state[node] = 1;

        for (int neighbor : graph.get(node)) {
            if (dfs(neighbor, graph, state)) {
                return true;
            }
        }

        state[node] = 2;

        return false;
    }

---

# 31. Directed Graph Cycle Detection Using Kahn's Algorithm

Kahn's algorithm uses topological sorting.

If a directed graph contains a cycle, not all nodes can be removed through indegree processing.

## Approach

1. Calculate indegree for every node.
2. Add all nodes with indegree `0` to a queue.
3. Remove nodes from the queue.
4. Reduce the indegree of their neighbors.
5. Add newly zero-indegree nodes.
6. Count processed nodes.

If:

    processedNodes < totalNodes

Then the graph contains a cycle.

Java:

    int[] indegree = new int[n];

    for (int u = 0; u < n; u++) {
        for (int v : graph.get(u)) {
            indegree[v]++;
        }
    }

    Queue<Integer> queue = new LinkedList<>();

    for (int i = 0; i < n; i++) {
        if (indegree[i] == 0) {
            queue.offer(i);
        }
    }

    int processed = 0;

    while (!queue.isEmpty()) {
        int node = queue.poll();
        processed++;

        for (int neighbor : graph.get(node)) {
            indegree[neighbor]--;

            if (indegree[neighbor] == 0) {
                queue.offer(neighbor);
            }
        }
    }

    boolean hasCycle = processed != n;

---

# 32. Topological Sorting

Topological sorting gives a linear ordering of vertices in a directed acyclic graph.

For every directed edge:

    A → B

`A` must appear before `B`.

Example:

    A → C
    B → C

Possible topological order:

    A, B, C

Another valid order:

    B, A, C

Topological sorting is only possible for DAGs.

---

# 33. Topological Sort Using Kahn's Algorithm

Kahn's algorithm is BFS-based.

## Steps

1. Calculate indegrees.
2. Add all zero-indegree nodes to a queue.
3. Remove a node.
4. Add it to the result.
5. Decrease indegrees of neighbors.
6. Add newly zero-indegree nodes.

Java:

    List<Integer> topoSort(int n, List<List<Integer>> graph) {
        int[] indegree = new int[n];

        for (int u = 0; u < n; u++) {
            for (int v : graph.get(u)) {
                indegree[v]++;
            }
        }

        Queue<Integer> queue = new LinkedList<>();

        for (int i = 0; i < n; i++) {
            if (indegree[i] == 0) {
                queue.offer(i);
            }
        }

        List<Integer> order = new ArrayList<>();

        while (!queue.isEmpty()) {
            int node = queue.poll();
            order.add(node);

            for (int neighbor : graph.get(node)) {
                indegree[neighbor]--;

                if (indegree[neighbor] == 0) {
                    queue.offer(neighbor);
                }
            }
        }

        if (order.size() != n) {
            return new ArrayList<>();
        }

        return order;
    }

Time complexity:

    O(V + E)

---

# 34. Topological Sort Using DFS

DFS-based topological sorting uses a stack.

## Idea

1. Visit a node.
2. Visit all its unvisited neighbors.
3. After processing all neighbors, push the node onto a stack.
4. Reverse finishing order gives the topological ordering.

Java:

    void dfsTopo(int node,
                 List<List<Integer>> graph,
                 boolean[] visited,
                 Stack<Integer> stack) {

        visited[node] = true;

        for (int neighbor : graph.get(node)) {
            if (!visited[neighbor]) {
                dfsTopo(neighbor, graph, visited, stack);
            }
        }

        stack.push(node);
    }

Then:

    for (int i = 0; i < n; i++) {
        if (!visited[i]) {
            dfsTopo(i, graph, visited, stack);
        }
    }

    List<Integer> result = new ArrayList<>();

    while (!stack.isEmpty()) {
        result.add(stack.pop());
    }

For cycle detection, use the three-state technique instead of only a boolean visited array.

---

# 35. Course Schedule Pattern

Typical problem:

There are `numCourses` courses and prerequisite pairs.

If:

    [A, B]

It means:

    B must be completed before A.

Create a directed edge:

    B → A

Then ask whether all courses can be completed.

## Solution

- Build the graph.
- Detect a directed cycle.
- If there is a cycle, return false.
- Otherwise, return true.

Kahn's algorithm is often straightforward.

---

# 36. Course Schedule II Pattern

Instead of checking whether courses can be completed, return a valid ordering.

Use topological sort.

If the resulting ordering contains fewer than `n` courses, return an empty array because a cycle exists.

---

# 37. Shortest Path Concepts

Shortest path means finding the minimum cost or minimum distance from one node to another.

The correct algorithm depends on graph properties.

| Graph Type | Best Common Algorithm |
|---|---|
| Unweighted graph | BFS |
| Weighted graph with non-negative weights | Dijkstra |
| DAG with weights | Topological-order shortest path |
| Graph with negative edge weights | Bellman-Ford |
| All-pairs shortest path | Floyd-Warshall |

---

# 38. BFS for Shortest Path in an Unweighted Graph

If every edge has equal cost:

    A --- B --- C

The shortest path from `A` to `C` has length `2`.

BFS guarantees the shortest number of edges because it explores nodes by increasing distance.

Template:

    Queue<Integer> queue = new LinkedList<>();
    int[] distance = new int[n];

    Arrays.fill(distance, -1);

    distance[start] = 0;
    queue.offer(start);

    while (!queue.isEmpty()) {
        int node = queue.poll();

        for (int neighbor : graph.get(node)) {
            if (distance[neighbor] == -1) {
                distance[neighbor] = distance[node] + 1;
                queue.offer(neighbor);
            }
        }
    }

---

# 39. Dijkstra's Algorithm

Dijkstra finds shortest paths from one source in a weighted graph with non-negative edge weights.

Example:

    A --4-- B
    |       |
    1       2
    |       |
    C --5-- D

Dijkstra repeatedly chooses the unprocessed node with the smallest known distance.

## Important Restriction

Dijkstra does not work correctly with negative edge weights.

## Core Idea

1. Initialize all distances to infinity.
2. Set source distance to `0`.
3. Put the source in a min-priority queue.
4. Extract the node with the smallest distance.
5. Relax all outgoing edges.
6. Repeat.

---

# 40. Relaxation

For an edge:

    u → v with weight w

If:

    distance[u] + w < distance[v]

Then update:

    distance[v] = distance[u] + w

This process is called relaxation.

Example:

    distance[A] = 0
    edge A → B has weight 4

Then:

    distance[B] = min(distance[B], 0 + 4)

---

# 41. Dijkstra Java Template

    int[] dijkstra(int n, List<List<Edge>> graph, int source) {

        int[] dist = new int[n];
        Arrays.fill(dist, Integer.MAX_VALUE);

        PriorityQueue<int[]> pq =
            new PriorityQueue<>((a, b) -> Integer.compare(a[1], b[1]));

        dist[source] = 0;
        pq.offer(new int[]{source, 0});

        while (!pq.isEmpty()) {
            int[] current = pq.poll();

            int node = current[0];
            int distance = current[1];

            if (distance > dist[node]) {
                continue;
            }

            for (Edge edge : graph.get(node)) {
                int next = edge.to;
                int weight = edge.weight;

                if (dist[node] != Integer.MAX_VALUE &&
                    dist[node] + weight < dist[next]) {

                    dist[next] = dist[node] + weight;
                    pq.offer(new int[]{next, dist[next]});
                }
            }
        }

        return dist;
    }

---

# 42. Why Does Dijkstra Use a Priority Queue?

At every step, Dijkstra needs the unprocessed node with the smallest tentative distance.

A priority queue provides this efficiently.

Without a priority queue:

- Finding the minimum node repeatedly can take `O(V²)`.

With a binary heap priority queue:

    Time ≈ O((V + E) log V)

Often simplified to:

    O(E log V)

for connected graphs.

Space:

    O(V + E)

---

# 43. The Stale Entry Optimization in Dijkstra

Java's `PriorityQueue` does not automatically update old entries.

Suppose a node is inserted with distance `10`, then later improved to `5`.

Both entries may remain in the queue.

When processing:

    int[] current = pq.poll();

Skip outdated entries:

    if (distance > dist[node]) {
        continue;
    }

This prevents unnecessary processing.

---

# 44. Dijkstra with Path Reconstruction

Sometimes the problem asks for the actual shortest path, not just the distance.

Maintain a parent array.

When relaxing an edge:

    parent[next] = node;

After reaching the destination, reconstruct by following parents backward.

Java pattern:

    int[] parent = new int[n];
    Arrays.fill(parent, -1);

    parent[next] = node;

Reconstruction:

    List<Integer> path = new ArrayList<>();

    int current = destination;

    while (current != -1) {
        path.add(current);
        current = parent[current];
    }

    Collections.reverse(path);

---

# 45. 0-1 BFS

Use 0-1 BFS when edge weights are only `0` or `1`.

Instead of a priority queue, use a deque.

Rules:

- Weight `0`: Add to the front.
- Weight `1`: Add to the back.

Java pattern:

    Deque<Integer> deque = new ArrayDeque<>();

    deque.offerFirst(source);

    while (!deque.isEmpty()) {
        int node = deque.pollFirst();

        for (Edge edge : graph.get(node)) {
            if (edge.weight == 0) {
                deque.offerFirst(edge.to);
            } else {
                deque.offerLast(edge.to);
            }
        }
    }

Time complexity:

    O(V + E)

---

# 46. Bellman-Ford Algorithm

Bellman-Ford handles negative edge weights.

It can also detect negative cycles reachable from the source.

## Idea

Relax every edge `V - 1` times.

Why `V - 1`?

A simple shortest path can contain at most `V - 1` edges.

Java:

    int[] dist = new int[n];
    Arrays.fill(dist, Integer.MAX_VALUE);

    dist[source] = 0;

    for (int i = 1; i <= n - 1; i++) {
        for (int[] edge : edges) {
            int u = edge[0];
            int v = edge[1];
            int weight = edge[2];

            if (dist[u] != Integer.MAX_VALUE &&
                dist[u] + weight < dist[v]) {

                dist[v] = dist[u] + weight;
            }
        }
    }

To detect a negative cycle, perform one additional relaxation pass.

If any distance can still be improved, a negative cycle exists.

Time complexity:

    O(VE)

---

# 47. Floyd-Warshall Algorithm

Floyd-Warshall finds shortest paths between every pair of vertices.

It uses dynamic programming.

Recurrence:

    dist[i][j] =
        min(
            dist[i][j],
            dist[i][k] + dist[k][j]
        )

Interpretation:

Should the shortest path from `i` to `j` pass through intermediate vertex `k`?

Time complexity:

    O(V³)

Space complexity:

    O(V²)

Useful when:

- The graph is small.
- All-pairs shortest paths are required.
- The graph is dense.

---

# 48. Minimum Spanning Tree (MST)

A Minimum Spanning Tree is a subset of edges in a connected, weighted, undirected graph that:

- Connects all vertices.
- Contains no cycles.
- Has minimum possible total edge weight.

For `V` vertices, every spanning tree has:

    V - 1 edges

Example:

    A --1-- B
    |       |
    4       2
    |       |
    C --3-- D

An MST chooses the cheapest set of edges connecting every node.

---

# 49. Prim's Algorithm

Prim's algorithm grows one connected tree.

## Idea

1. Start from any vertex.
2. Add the cheapest edge connecting the current tree to an unvisited vertex.
3. Continue until all vertices are included.

It uses a min-priority queue.

Java idea:

    PriorityQueue<int[]> pq =
        new PriorityQueue<>((a, b) -> Integer.compare(a[1], b[1]));

    boolean[] visited = new boolean[n];

    pq.offer(new int[]{0, 0});

    int totalCost = 0;

    while (!pq.isEmpty()) {
        int[] current = pq.poll();

        int node = current[0];
        int weight = current[1];

        if (visited[node]) {
            continue;
        }

        visited[node] = true;
        totalCost += weight;

        for (Edge edge : graph.get(node)) {
            if (!visited[edge.to]) {
                pq.offer(new int[]{edge.to, edge.weight});
            }
        }
    }

Time complexity with adjacency list and heap:

    O(E log V)

---

# 50. Kruskal's Algorithm

Kruskal's algorithm builds an MST by considering edges globally.

## Idea

1. Sort all edges by weight.
2. Add the next cheapest edge if it does not create a cycle.
3. Continue until `V - 1` edges are selected.

To efficiently detect cycles, use Disjoint Set Union.

---

# 51. Disjoint Set Union (DSU) / Union-Find

DSU maintains groups of connected components.

It supports two main operations:

- `find(x)`: Find the representative/root of the component containing `x`.
- `union(a, b)`: Merge the components containing `a` and `b`.

Used in:

- Kruskal's MST.
- Dynamic connectivity.
- Redundant connection.
- Number of connected components.
- Detecting cycles in undirected graphs.

---

# 52. DSU with Path Compression and Union by Size

Java:

    class DSU {
        int[] parent;
        int[] size;

        DSU(int n) {
            parent = new int[n];
            size = new int[n];

            for (int i = 0; i < n; i++) {
                parent[i] = i;
                size[i] = 1;
            }
        }

        int find(int x) {
            if (parent[x] != x) {
                parent[x] = find(parent[x]);
            }

            return parent[x];
        }

        boolean union(int a, int b) {
            int rootA = find(a);
            int rootB = find(b);

            if (rootA == rootB) {
                return false;
            }

            if (size[rootA] < size[rootB]) {
                int temp = rootA;
                rootA = rootB;
                rootB = temp;
            }

            parent[rootB] = rootA;
            size[rootA] += size[rootB];

            return true;
        }
    }

With both optimizations:

    Amortized time per operation = O(α(V))

`α(V)` is the inverse Ackermann function and is effectively constant for practical input sizes.

---

# 53. Kruskal Java Template

    int kruskal(int n, int[][] edges) {

        Arrays.sort(edges,
            (a, b) -> Integer.compare(a[2], b[2]));

        DSU dsu = new DSU(n);

        int totalWeight = 0;
        int edgesUsed = 0;

        for (int[] edge : edges) {
            int u = edge[0];
            int v = edge[1];
            int weight = edge[2];

            if (dsu.union(u, v)) {
                totalWeight += weight;
                edgesUsed++;

                if (edgesUsed == n - 1) {
                    break;
                }
            }
        }

        return totalWeight;
    }

---

# 54. Prim vs Kruskal

| Feature | Prim | Kruskal |
|---|---|---|
| Strategy | Grows one tree | Selects globally cheapest edges |
| Main structure | Priority Queue | Sorting + DSU |
| Best representation | Adjacency list | Edge list |
| Cycle handling | Visited array | DSU |
| Typical complexity | O(E log V) | O(E log E) |
| Good for | Dense graphs | Sparse graphs / edge-list input |

---

# 55. Bipartite Graph

A graph is bipartite if its vertices can be divided into two groups such that no edge connects vertices within the same group.

Equivalent condition:

A graph is bipartite if it can be colored using two colors without adjacent vertices having the same color.

Example:

    A --- B
    |     |
    C --- D

One coloring:

- Group 1: `A, D`
- Group 2: `B, C`

---

# 56. Bipartite Check Using BFS

Use two colors:

- `0` = Uncolored
- `1` = Color A
- `-1` = Color B

Java:

    boolean isBipartite(List<List<Integer>> graph) {

        int n = graph.size();
        int[] color = new int[n];

        Arrays.fill(color, -1);

        for (int start = 0; start < n; start++) {

            if (color[start] != -1) {
                continue;
            }

            Queue<Integer> queue = new LinkedList<>();
            queue.offer(start);
            color[start] = 0;

            while (!queue.isEmpty()) {
                int node = queue.poll();

                for (int neighbor : graph.get(node)) {

                    if (color[neighbor] == -1) {
                        color[neighbor] = 1 - color[node];
                        queue.offer(neighbor);

                    } else if (color[neighbor] == color[node]) {
                        return false;
                    }
                }
            }
        }

        return true;
    }

---

# 57. Bipartite Check Using DFS

    boolean dfs(int node,
                int currentColor,
                List<List<Integer>> graph,
                int[] color) {

        color[node] = currentColor;

        for (int neighbor : graph.get(node)) {

            if (color[neighbor] == -1) {
                if (!dfs(neighbor,
                         1 - currentColor,
                         graph,
                         color)) {
                    return false;
                }

            } else if (color[neighbor] == currentColor) {
                return false;
            }
        }

        return true;
    }

---

# 58. Important Bipartite Insight

An undirected graph is bipartite if and only if it contains no odd-length cycle.

Examples:

- A triangle is not bipartite.
- A square is bipartite.
- Any tree is bipartite.

---

# 59. Graph Coloring

Graph coloring assigns colors to vertices such that adjacent vertices have different colors.

Two-coloring is exactly the bipartite problem.

General graph coloring with a fixed number of colors can be difficult and is often NP-complete.

In interviews, common versions include:

- Two-coloring.
- Bipartite checking.
- Scheduling conflicts.
- Register allocation variations.

---

# 60. Flood Fill

Flood Fill is a graph traversal problem on a grid.

Starting from one cell, change all connected cells having the same original value.

Example:

    1 1 1
    1 1 0
    1 0 1

Starting at `(0, 0)`, change all connected `1`s.

Use DFS or BFS.

Java:

    void floodFill(int[][] image,
                   int sr,
                   int sc,
                   int newColor) {

        int original = image[sr][sc];

        if (original == newColor) {
            return;
        }

        dfs(image, sr, sc, original, newColor);
    }

    void dfs(int[][] image,
             int r,
             int c,
             int original,
             int newColor) {

        int rows = image.length;
        int cols = image[0].length;

        if (r < 0 || r >= rows ||
            c < 0 || c >= cols ||
            image[r][c] != original) {
            return;
        }

        image[r][c] = newColor;

        dfs(image, r + 1, c, original, newColor);
        dfs(image, r - 1, c, original, newColor);
        dfs(image, r, c + 1, original, newColor);
        dfs(image, r, c - 1, original, newColor);
    }

---

# 61. Rotting Oranges Pattern

This is a multi-source BFS problem.

## Idea

- Add all initially rotten oranges to the queue.
- Each BFS level represents one minute.
- Spread rot to adjacent fresh oranges.
- Count remaining fresh oranges.

Important:

Do not run separate BFS from each rotten orange.

All rotten oranges must be processed simultaneously.

---

# 62. Word Ladder Pattern

Word Ladder is a shortest-path problem.

Each word is a node.

An edge exists between two words if they differ by one character.

Because every transformation costs one step, use BFS.

Typical approach:

1. Store dictionary words in a set.
2. Start BFS from the beginning word.
3. Generate all one-letter transformations.
4. If a generated word exists in the set, visit it.
5. Stop when the target word is reached.

---

# 63. Snakes and Ladders Pattern

Treat board positions as graph nodes.

From each position, there are up to six possible dice moves.

A snake or ladder changes the destination position.

Since each dice roll has equal cost, BFS finds the minimum number of rolls.

---

# 64. Clone Graph

Given a reference to a graph node, create a deep copy of the entire graph.

## Approach

Use DFS or BFS plus a map.

The map stores:

    original node → cloned node

This prevents:

- Infinite recursion due to cycles.
- Creating multiple clones of the same node.

Java pattern:

    Map<Node, Node> map = new HashMap<>();

    Node clone(Node node) {

        if (node == null) {
            return null;
        }

        if (map.containsKey(node)) {
            return map.get(node);
        }

        Node copy = new Node(node.val);
        map.put(node, copy);

        for (Node neighbor : node.neighbors) {
            copy.neighbors.add(clone(neighbor));
        }

        return copy;
    }

---

# 65. Alien Dictionary Pattern

The Alien Dictionary problem asks for character ordering from a sorted list of words in an unknown language.

## Approach

1. Compare adjacent words.
2. Find the first differing character.
3. Add a directed edge from the character in the first word to the character in the second word.
4. Topologically sort the resulting graph.

Important invalid case:

If a longer word appears before its exact prefix:

    ["abc", "ab"]

Then no valid ordering exists.

---

# 66. Redundant Connection

Given an undirected graph formed by adding one extra edge to a tree, find the redundant edge.

A tree with `n` nodes has exactly `n - 1` edges.

The extra edge creates a cycle.

Use DSU:

- If `union(u, v)` succeeds, continue.
- If `union(u, v)` returns false, `u` and `v` are already connected.
- That edge is redundant.

---

# 67. Network Delay Time

Given a weighted directed graph and a starting node, determine how long it takes for a signal to reach every node.

Use Dijkstra because edge weights are non-negative.

Answer:

    Maximum shortest-path distance among all nodes.

If any node remains unreachable:

    return -1

---

# 68. Cheapest Flights Within K Stops

This is a shortest-path variation with a stop constraint.

Regular Dijkstra may need modification because a path with a lower cost may use too many stops.

Common approaches:

- Modified BFS for limited levels.
- Bellman-Ford for at most `K + 1` edges.
- Priority queue storing `(cost, node, stops)`.

Track the number of stops used.

---

# 69. Path With Minimum Effort

In a grid, moving between adjacent cells has an effort equal to the absolute difference in heights.

The cost of a path is the maximum edge effort along that path.

This is not a normal sum-of-weights shortest path.

Use modified Dijkstra:

    newEffort = max(currentEffort, edgeEffort)

Relax if:

    newEffort < dist[next]

---

# 70. Cheapest Path / Minimum Cost Patterns

Always identify what the path cost means.

## Sum of Edge Weights

Use standard shortest-path algorithms.

Example:

    cost = 2 + 5 + 1

## Maximum Edge Weight Along a Path

Use modified Dijkstra.

Example:

    cost = max(2, 5, 1) = 5

## Number of Edges

Use BFS if unweighted.

## Limited Number of Stops

Use BFS, Bellman-Ford, or state-based Dijkstra.

---

# 71. Graph Problem Decision Tree

## Step 1: Is it a graph?

Look for:

- Nodes and relationships.
- Cities and roads.
- Courses and prerequisites.
- People and connections.
- Grid cells and neighboring cells.
- State transformations.

## Step 2: Directed or undirected?

- Two-way relationship → Undirected.
- One-way dependency → Directed.

## Step 3: Weighted or unweighted?

- No cost / equal movement → Unweighted.
- Distances, times, prices → Weighted.

## Step 4: What is being asked?

### Explore all reachable nodes

Use DFS or BFS.

### Count connected groups

Use DFS, BFS, or DSU.

### Shortest path in unweighted graph

Use BFS.

### Shortest path with non-negative weights

Use Dijkstra.

### Negative weights

Use Bellman-Ford.

### All-pairs shortest path

Use Floyd-Warshall.

### Minimum spanning tree

Use Prim or Kruskal.

### Detect cycle in undirected graph

Use DFS with parent or DSU.

### Detect cycle in directed graph

Use recursion stack states or Kahn's algorithm.

### Dependency ordering

Use topological sort.

### Two-coloring

Use BFS or DFS coloring.

---

# 72. Common Graph Patterns

## Pattern 1: Reachability

Question:

Can node `A` reach node `B`?

Use DFS or BFS.

## Pattern 2: Connected Components

Question:

How many groups are there?

Use outer loop + DFS/BFS.

## Pattern 3: Shortest Unweighted Path

Question:

Minimum moves or edges?

Use BFS.

## Pattern 4: Multi-Source Spread

Question:

How long until everything spreads?

Use multi-source BFS.

## Pattern 5: Directed Dependencies

Question:

Can tasks be completed? What ordering is valid?

Use cycle detection or topological sort.

## Pattern 6: Weighted Shortest Path

Question:

Minimum cost or distance?

Use Dijkstra if weights are non-negative.

## Pattern 7: Minimum Total Connection Cost

Question:

Connect all nodes as cheaply as possible.

Use MST.

## Pattern 8: Dynamic Connectivity

Question:

Are two nodes connected after multiple union operations?

Use DSU.

## Pattern 9: Two-Group Assignment

Question:

Can nodes be divided into two groups with no conflicts?

Use bipartite coloring.

---

# 73. Graph Complexity Cheat Sheet

| Algorithm | Time Complexity | Space Complexity | Main Use |
|---|---:|---:|---|
| BFS | O(V + E) | O(V) | Traversal / shortest unweighted path |
| DFS | O(V + E) | O(V) | Traversal / components / cycles |
| Topological Sort | O(V + E) | O(V) | DAG ordering |
| Kahn Cycle Detection | O(V + E) | O(V) | Directed cycle detection |
| Dijkstra with Heap | O((V + E) log V) | O(V + E) | Non-negative weighted shortest path |
| Bellman-Ford | O(VE) | O(V) | Negative edge weights |
| Floyd-Warshall | O(V³) | O(V²) | All-pairs shortest paths |
| Prim with Heap | O(E log V) | O(V + E) | MST |
| Kruskal | O(E log E) | O(V) | MST |
| DSU Operation | O(α(V)) amortized | O(V) | Connectivity |
| Bipartite Check | O(V + E) | O(V) | Two-coloring |

---

# 74. Graph Representation Complexity

| Operation | Adjacency List | Adjacency Matrix |
|---|---:|---:|
| Space | O(V + E) | O(V²) |
| Check edge | O(degree) | O(1) |
| Iterate neighbors | O(degree) | O(V) |
| Add edge | O(1) | O(1) |
| Remove edge | O(degree) | O(1) |

For most interview problems, use adjacency lists unless the graph is very dense or the input is naturally a matrix.

---

# 75. Java Graph Coding Template

A reusable undirected graph template:

    import java.util.*;

    class Solution {

        public List<List<Integer>> buildGraph(
                int n,
                int[][] edges) {

            List<List<Integer>> graph = new ArrayList<>();

            for (int i = 0; i < n; i++) {
                graph.add(new ArrayList<>());
            }

            for (int[] edge : edges) {
                int u = edge[0];
                int v = edge[1];

                graph.get(u).add(v);
                graph.get(v).add(u);
            }

            return graph;
        }

        public void dfs(int node,
                        List<List<Integer>> graph,
                        boolean[] visited) {

            visited[node] = true;

            for (int neighbor : graph.get(node)) {
                if (!visited[neighbor]) {
                    dfs(neighbor, graph, visited);
                }
            }
        }

        public void bfs(int start,
                        List<List<Integer>> graph,
                        boolean[] visited) {

            Queue<Integer> queue = new LinkedList<>();

            queue.offer(start);
            visited[start] = true;

            while (!queue.isEmpty()) {
                int node = queue.poll();

                for (int neighbor : graph.get(node)) {
                    if (!visited[neighbor]) {
                        visited[neighbor] = true;
                        queue.offer(neighbor);
                    }
                }
            }
        }
    }

---

# 76. Common Java Mistakes

## Mistake 1: Forgetting Reverse Edges

For an undirected graph:

    graph.get(u).add(v);
    graph.get(v).add(u);

Both are required.

## Mistake 2: Forgetting Visited Tracking

Always prevent revisiting nodes.

## Mistake 3: Starting Only From One Node

For disconnected graphs, use:

    for (int i = 0; i < n; i++) {
        if (!visited[i]) {
            dfs(i, graph, visited);
        }
    }

## Mistake 4: Using BFS for Weighted Shortest Path

BFS only guarantees shortest paths when all edges have equal cost.

## Mistake 5: Using Dijkstra With Negative Edges

Dijkstra requires non-negative edge weights.

## Mistake 6: Forgetting Parent in Undirected Cycle Detection

A visited parent is not automatically a cycle.

## Mistake 7: Forgetting Recursion Stack State in Directed Cycle Detection

A normal visited array cannot distinguish between:

- Currently processing a node.
- Fully processed node.

## Mistake 8: Not Handling Duplicate Priority Queue Entries

In Dijkstra, skip stale entries:

    if (distance > dist[node]) {
        continue;
    }

## Mistake 9: Integer Overflow

When using large distances:

    long[] dist = new long[n];

Avoid adding weights to `Integer.MAX_VALUE`.

---

# 77. Interview Explanation Template

When explaining a graph solution, follow this structure:

## Step 1: Identify the Graph

"Each entity represents a node, and each relationship represents an edge."

## Step 2: Identify Graph Type

"This is an undirected/directed weighted/unweighted graph."

## Step 3: Choose Representation

"I will use an adjacency list because the graph is sparse and I need to iterate over neighbors."

## Step 4: Explain Algorithm Choice

"I will use BFS because every edge has equal cost and we need the minimum number of steps."

Or:

"I will use DFS because we need to explore connected components."

Or:

"I will use Dijkstra because edge weights are non-negative and we need minimum total cost."

## Step 5: Explain Visited / State

"I mark a node when I first discover it so I do not process it repeatedly."

## Step 6: Complexity

"For an adjacency list, every vertex and edge is processed at most once, so time is O(V + E) and space is O(V + E) for the graph plus O(V) traversal space."

---

# 78. How to Recognize Graph Problems Quickly

A problem may not explicitly say "graph."

Look for hidden graphs.

## Grid Problems

Cells are nodes.

Neighbors are edges.

Examples:

- Number of Islands
- Flood Fill
- Rotting Oranges
- Word Search variations
- Walls and Gates

## String Transformation Problems

Words or strings are nodes.

One valid transformation creates an edge.

Examples:

- Word Ladder
- Minimum genetic mutation

## Scheduling Problems

Tasks are nodes.

Prerequisites are directed edges.

Examples:

- Course Schedule
- Build systems
- Task scheduling

## Social Network Problems

People are nodes.

Relationships are edges.

Examples:

- Friend circles
- Number of provinces
- Recommendation networks

## State-Space Problems

Each possible state is a node.

A legal operation creates an edge.

Examples:

- Lock combinations
- Snakes and Ladders
- Puzzle transformations

---

# 79. Graph Theory Interview Checklist

## Fundamentals

- [ ] Can I explain vertices and edges?
- [ ] Can I distinguish directed and undirected graphs?
- [ ] Can I distinguish weighted and unweighted graphs?
- [ ] Do I know what a DAG is?
- [ ] Do I understand connected components?
- [ ] Do I know what a cycle is?
- [ ] Do I understand degree, indegree, and outdegree?

## Representation

- [ ] Can I build an adjacency list?
- [ ] Can I build an adjacency matrix?
- [ ] Do I know when to use an edge list?
- [ ] Can I represent weighted edges?
- [ ] Do I understand O(V + E) graph storage?

## Traversal

- [ ] Can I write recursive DFS?
- [ ] Can I write iterative DFS?
- [ ] Can I write BFS using a queue?
- [ ] Can I track visited nodes correctly?
- [ ] Can I handle disconnected graphs?
- [ ] Can I perform multi-source BFS?
- [ ] Can I track BFS levels and distances?

## Connected Components and Grid Problems

- [ ] Can I count connected components?
- [ ] Can I solve Number of Islands?
- [ ] Can I solve Flood Fill?
- [ ] Can I identify valid grid directions?
- [ ] Can I avoid revisiting grid cells?

## Cycle Detection

- [ ] Can I detect cycles in an undirected graph using DFS?
- [ ] Can I detect cycles in an undirected graph using BFS?
- [ ] Can I detect cycles using DSU?
- [ ] Can I detect cycles in a directed graph using DFS states?
- [ ] Can I detect cycles in a directed graph using Kahn's algorithm?

## Topological Sorting

- [ ] Do I understand what a DAG is?
- [ ] Can I calculate indegrees?
- [ ] Can I implement Kahn's algorithm?
- [ ] Can I implement DFS-based topological sorting?
- [ ] Can I solve Course Schedule?
- [ ] Can I solve Course Schedule II?
- [ ] Can I detect invalid prefix cases in Alien Dictionary?

## Shortest Paths

- [ ] Do I know when BFS is enough?
- [ ] Can I implement Dijkstra?
- [ ] Do I understand relaxation?
- [ ] Can I use a priority queue correctly?
- [ ] Can I skip stale Dijkstra entries?
- [ ] Do I know why Dijkstra fails with negative edges?
- [ ] Do I understand 0-1 BFS?
- [ ] Can I explain Bellman-Ford?
- [ ] Do I understand Floyd-Warshall?
- [ ] Can I reconstruct a shortest path?

## Minimum Spanning Trees

- [ ] Do I understand what an MST is?
- [ ] Can I implement Prim's algorithm?
- [ ] Can I implement Kruskal's algorithm?
- [ ] Can I implement DSU?
- [ ] Do I understand path compression?
- [ ] Do I understand union by size/rank?

## Bipartite Graphs

- [ ] Can I explain bipartite graphs?
- [ ] Can I implement two-coloring using BFS?
- [ ] Can I implement two-coloring using DFS?
- [ ] Do I know the odd-cycle property?

## Advanced Patterns

- [ ] Can I solve Word Ladder using BFS?
- [ ] Can I solve Rotting Oranges using multi-source BFS?
- [ ] Can I solve Network Delay Time using Dijkstra?
- [ ] Can I solve Cheapest Flights Within K Stops?
- [ ] Can I solve Path With Minimum Effort?
- [ ] Can I solve Redundant Connection using DSU?
- [ ] Can I clone a graph using DFS and a map?

---

# 80. Final Graph Theory Revision Summary

## Memorize These Core Templates

### DFS

    void dfs(int node) {
        visited[node] = true;

        for (int neighbor : graph.get(node)) {
            if (!visited[neighbor]) {
                dfs(neighbor);
            }
        }
    }

### BFS

    Queue<Integer> queue = new LinkedList<>();

    queue.offer(start);
    visited[start] = true;

    while (!queue.isEmpty()) {
        int node = queue.poll();

        for (int neighbor : graph.get(node)) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                queue.offer(neighbor);
            }
        }
    }

### Disconnected Graph

    for (int i = 0; i < n; i++) {
        if (!visited[i]) {
            dfs(i);
        }
    }

### Undirected Cycle Detection

    if (!visited[neighbor]) {
        dfs(neighbor, node);
    } else if (neighbor != parent) {
        return true;
    }

### Directed Cycle Detection

    if (state[node] == 1) {
        return true;
    }

    state[node] = 1;

    for (int neighbor : graph.get(node)) {
        if (dfs(neighbor)) {
            return true;
        }
    }

    state[node] = 2;

### Topological Sort

    Calculate indegrees.
    Add zero-indegree nodes to queue.
    Process queue.
    Decrease neighbor indegrees.
    If all nodes are processed, no cycle exists.

### Dijkstra

    dist[source] = 0;
    Push source into min-heap.

    while (!pq.isEmpty()) {
        Remove node with smallest distance.

        For every edge:
            Relax the edge.
            Push improved distance.
    }

### DSU

    find(x):
        Return representative/root.

    union(a, b):
        Merge roots if different.
        If already same root, adding the edge creates a cycle.

---

# 81. Final Interview Strategy

When you see a graph problem, ask these questions in order:

1. What are the nodes?
2. What are the edges?
3. Is the graph directed or undirected?
4. Is it weighted or unweighted?
5. Is the graph connected or potentially disconnected?
6. Do I need to visit everything?
7. Do I need the shortest path?
8. Is shortest path based on number of edges or total weight?
9. Are there cycles?
10. Is there a dependency ordering?
11. Do I need a minimum spanning tree?
12. Can DSU simplify connectivity?
13. Is this actually a hidden graph such as a grid or state-space problem?

## Quick Algorithm Selection

| Requirement | Algorithm |
|---|---|
| Visit all reachable nodes | DFS / BFS |
| Count groups | DFS / BFS / DSU |
| Shortest path, equal edge cost | BFS |
| Shortest path, non-negative weights | Dijkstra |
| Shortest path, weights 0 and 1 | 0-1 BFS |
| Negative edge weights | Bellman-Ford |
| All-pairs shortest paths | Floyd-Warshall |
| Detect undirected cycle | DFS + parent / BFS + parent / DSU |
| Detect directed cycle | DFS states / Kahn's algorithm |
| Dependency ordering | Topological sort |
| Connect all nodes cheaply | Prim / Kruskal |
| Two-coloring | Bipartite BFS / DFS |
| Dynamic connectivity | DSU |

## The Most Important Interview Rule

Do not immediately choose an algorithm because the problem contains nodes and edges.

First identify the exact requirement:

- Exploration → DFS/BFS
- Minimum number of steps → BFS
- Minimum weighted cost → Dijkstra
- Dependencies → Topological Sort
- Cheapest way to connect everything → MST
- Connectivity under unions → DSU
- Conflict between two groups → Bipartite Coloring

Once the graph type and required operation are clear, the algorithm usually becomes obvious.