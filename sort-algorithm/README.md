# Sort Algorithm 排序

## 1 Sorting Algorithm 

Bubble Sort, T: $O\(n^2\)$, S: $O\(1\)$ 

Insertion Sort, $O\(n^2\)$, S: $O\(1\)$ 

Heap Sort, $O\(n \log n\)$, S: $\(1\)$ 

Quick Sort, $O\(n \log n\)$, S: $O\(1\)$ 

Merge Sort, $O\(n \log n\)$, S: $O\(n\)$

## 2 Quick Sort vs. Merge Sort

### A Few Comments

Quick Sort: space $O\(1\)$

Merge Sort: need extra space $O\(n\)$, and creating/deleting space is expensive operation --&gt; in practice, much slower 

Quick Sort: avg. $O\(n\log\(n\)\)$, worst case $O\(n^2\)$, e.g. when array is in descending order, and you always pick first element as pivot 

Merge Sort: avg. $O\(n\log\(n\)\)$, worst case $O\(n\log n\)$ 

Quick Sort: not stable sort - save value at different index, the index order is not preserved; easy fix for quick sort if we want: custom comparater on \(val, idx\) 

Merge Sort: stable sort automatically

### In Terms of Divide and Conquer

Both Quick Sort and Merge Sort are doing divide and conquer, but they differ slightly 

Quick Sort: make order at macro level, and then make order at micro level 

Merge Sort: make order at micro level, and then make order at macro level 

Quick Sort: $T\(n\) = O\(n\) + 2T\(n/2\)$ 

Merge Sort: $T\(n\) = 2T\(n/2\) + O\(n\)$

