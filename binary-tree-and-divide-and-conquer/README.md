# Binary Tree and Divide & Conquer

1. **Divide & Conquer \(D & C\)**

Divide big problem into several similar and smaller problems   
****D&C vs. Binary Search

* Assime the process time is O\(1\)
* Divide & Conquer needs to process for both sides after the divide. O\(n\)
* Binary Search throws away half side after the divide O\(log n\)
* Array \(divide big array into disjoint subarrays\)
* Linked List \(not that good, need to O\(n\) to find the cutting point\)
* Binary Tree \(most natural, it has left and right sub-tree\)

Most Binary tree questions could be solved by Divide & Conquer

A few Concepts about search

Recursions, DFS, Backtracking, Traversal, D&C, Iteration

Search by orders \(depth first or breadth first\)

Backtracking is the step where we recover all the states when going back for a new forking - some times we need to manually recover the state, and in recursion, there is also automatic recovering of state when we come to the upper layer of stack of the OS. Thus in certain sense, DFS must has backtracking and they are equivalent.  
  
Different algorithm \(take different route\) for DFS: traversal vs D&C

Different implementation \(drive or walk\) for traversal or D&C:  
recursion vs. iteration





