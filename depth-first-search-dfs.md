# Depth First Search \(DFS\) 深度优先搜索

**1 When to use DFS**

One big application is for Binary Tree

Other application:

* Ask you to find ALL solutions, 90% - either combination\(O 2^n\) or arrangement \(O\(n!\)\)
* Find optimal solutions, 20% DFS, 80% dynamic programming
* Subsequence, may try DFS \(equivalent to combination search\), but more likely to be dynamic programming
* Substring, most unlikely \(substring search O\(n^2\), but DFS usually has 2^n\)

**Find all solutions that match a certain condition**

Equivalent to finding all paths that satisfy the condition in a graph

path == solution == arrangements of nodes in the graph

need to define points/edges/paths

**Find Subset**

Directed Graph  
point: elements in the set  
edges: the directed connection between elements, from smaller point to bigger point \(in order to avoid duplicated subset such as \(1,2\) and \(2,1\)  
paths: = subsets = paths starting from any points and ending at any point in the graph

![](.gitbook/assets/image%20%2813%29.png)

**Find permutation by N number**

Undirected Graph   
point: elements in the set   
edges: the undirected edge between elements  
paths:= permutation = paths starting from any point and ending at any point in the graph, while each node appears in the path exactly once  


![](.gitbook/assets/image%20%2815%29.png)

**2. Finding all solutions \(solution == path\): BFS vs. DFS**

![](.gitbook/assets/image%20%2814%29.png)

**Subset**  
  


![](.gitbook/assets/image%20%2816%29.png)

