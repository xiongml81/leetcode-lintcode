# Quick Sort of Array 快速排序

## 1.Question: Partition Array

Given an array nums of integers and an int k, partition the array \(i.e move the elements in "nums"\) such that: All elements &lt; k are moved to the left All elements &gt;= k are moved to the right Return the partitioning index, i.e the first index i nums\[i\] &gt;= k.   
Example 1: 

`Input: [],9   Output: 0` 

Example 2:

`Input: [3,2,2,1],2 Output:1`  
Explanation: the real array is\[1,2,2,3\]. So return 1

### 1.1 Code

```java
//[3,2,2,1], k = 2, return partition index, the first index i nums[i] >=k
//all elements < k on left, all elements >= k on right
public static int partition(int[] nums, int k) {
		int first = 0; int last = nums.length - 1;
		
		while(first <= last) {
			if(nums[first] < k) {
				first++;
			}
			else if(nums[last] >= k) {
				last--;
			}
			else {
				int temp = nums[first];
				nums[first] = nums[last];
				nums[last] = temp;
				first++;
				last--;
			}
		}
		
		return first;
	}
```

## 2.Quick Sort

### 2.1 Pick Pivot

Random pick \(usually not necessary, and there is cost associate with it to call rand\(\)\) Rule of thumb: take mid index

### 2.2 题目地址

[**https://leetcode.com/problems/sort-an-array/**](https://leetcode.com/problems/sort-an-array/)\*\*\*\*

### 2.3 Code

```java
public static int partition(int[] nums, int start, int end){
        int pivot = nums[start + (end - start) / 2];
        
        while(start <= end){
            if(nums[start] < pivot){
                start++;
            }
            else if(nums[end] > pivot){
                end--;
            }
            else{
                int temp = nums[start];
                nums[start] = nums[end];
                nums[end] = temp;
                start++;
                end--;
            }
        }
        
        return start;
    }

	
	public static void quickSort(int[] nums, int start, int end) {
		//base case
		if(start >= end) {
			return;
		}
	
		int pivotPosition = partition(nums, start, end);
		quickSort(nums, start, pivotPosition - 1);
		quickSort(nums, pivotPosition, end);
	}
```

### 2.4 Why not strict cut?

For quick sort, partition by pivot is done as: $ &lt;= P$ + $ &gt;= P$ \(num\[left\] &lt; pivot -&gt; no change, num\[left\] &gt;= pivot -&gt; move to right; num\[right\] &gt; pivot -&gt; no change, num\[right\] &lt;= pivot, move to left. So that it is balanced. e.g. \[11111111111\]: in this case, the "else" condition will be executed and when that happens, along with swap, both left and right point would move, so that we get balanced cut of the array When most/all of the elements are the same value, divide would be extremely unbalanced If each cut is very unbalaned: time complexity would be $O\(1\)$ Extreme case: all elements are equal, at each dvide, if we do $ &lt; P$ + $ &gt;= P$, then left: $0$; right: $n$ ==&gt; cannot exit

### 2.5 Why left &lt;= right?

e.g. nums = \[3, 2, 1, 4, 5\] Init: left -&gt; 3; right -&gt; 5, pivot =-&gt; 1 After a while: left -&gt; 3, right -&gt; 1; Swap: \[1, 2, 3, 4, 5\], left -&gt; 2, right -&gt; 2 Now do while big loop, no longer meet left &lt; right, exit Consequence: element 2 included in both sub-quick\_sorts Now let's focus on left sub-quick\_sorts on \[1, 2\] Init: left -&gt; 1; right -&gt; 2; After a while: left -&gt; 1; right -&gt; 1; Now do while big loop, no longer meet left &lt; right, exit Now right sub-quick\_sort still is \[1, 2\] - did not shrink; infinite recursion!!!

### 2.6 Why we cannot use the same code for partition array

Partition array requires to partition the array into two parts, one part satisfies certain condition, while the other part does not - thus there are some exclusions in the question

## 3. Extensions - Quick Select

Select Pivot \(mid index\) ==&gt; $\ge pivot + \le pivot$ Check is index $k$ on the left or right, and only need to look at exactly ONE side Time Complexity: Avg: $T\(n\) = T\(n\) + T\(n/2\) \rightarrow O\(n\)$, Worst: $O\(n^2\)$ Space Complexity: $O\(1\)$

### **3.1 Question: Find K-th largest element in an array**

### 3.2 题目

\*\*\*\*[**https://leetcode.com/problems/kth-largest-element-in-an-array/**](https://leetcode.com/problems/kth-largest-element-in-an-array/)\*\*\*\*

Find the **k**th largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

​Example 1：  
`Input: k = 1, nums = [1,3,4,2] Output: 4`  


Example 2：  
`Input: k = 3, nums = [9,3,2,4,8] Output: 4`

### 3.3 Code

```java
class Solution {
    //[1,2,3,4,5,6] k = 1
    public int findKthLargest(int[] nums, int k) {
        int start = 0; int end = nums.length - 1;
        int target = nums.length - k;
        int index = quickSelect(nums, 0, end, target);
        return nums[index];
    }
    
    public int partition(int[] nums, int first, int last){
        int pivot = nums[first + (last - first) / 2];
        while(first <= last){
            if(nums[first] < pivot){
                first++;
            }
            else if(nums[last] > pivot){
                last--;
            }
            else{
                int temp = nums[first];
                nums[first] = nums[last];
                nums[last] = temp;
                first++;
                last--;
            }
        }
        return first;
    }
    
    
    // 你的思路差不多，但是要注意返回的内容，partition返回了一个pivot，你只能确定的是：pivot左边的数（不包括pivot）小于等于partition中你的那个值，pivot右边的数（包含pivot）大于等于partition中的那个值，所以当pivot等于target的时候，并不是说pivot位置的数就是排好序后的pivot位置的数，你只是找到一个分界点而已，所以要返回的话，只能是在start和end相等的时候才能返回，所以你改成这样就可以了
    public int quickSelect(int[] nums, int start, int end, int target){
        if(start >= end) return start;
        
        int pivot = partition(nums, start, end);
        if(pivot > target){
              return quickSelect(nums, start, pivot - 1, target);
        }
        else {
             return quickSelect(nums, pivot, end, target);
           
        }
    }
}
```











