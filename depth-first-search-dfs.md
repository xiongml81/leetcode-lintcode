# Depth First Search \(DFS\) 深度优先搜索

**1 When to use DFS**

One big application is for Binary Tree

Other application:

* Ask you to find ALL solutions, 90% - either combination\(O 2^n\) or arrangement \(O\(n!\)\)
* Find optimal solutions, 20% DFS, 80% dynamic programming
* Subsequence, may try DFS \(equivalent to combination search\), but more likely to be dynamic programming
* Substring, most unlikely \(substring search O\(n^2\), but DFS usually has 2^n\)

**Find all solutions that matches certain condition**

Equivalent to finding all paths that satisfies the condition in a graph

path == solution == arrangements of nodes in the graph

need to defin points/edges/paths

**Find Subset**

Directed Graph

point: elements in the set

edges: directed connection between elements, from smaller point to bigger point \(in order to avoid duplicated subset such as \(1,2\) and \(2,1\)

