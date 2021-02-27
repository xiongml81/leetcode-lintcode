# Merge Sort of Array 归并排序

## 1. Question: Merge Sorted Array

Merge two given sorted ascending integer array A and B into a new sorted integer array.

Example 1:

`Input: A=[1], B=[1] Output: [1,1]` 

`Explanation: return array merged.`

Example 2:

`Input: A=[1,2,3,4], B=[2,4,5,6] Output: [1,2,2,3,4,4,5,6]` 

`Explanation: return array merged.`

### 1.1 Code

### 1.2 题目

\*\*\*\*

\*\*\*\*[**https://leetcode.com/problems/merge-sorted-array/**](https://leetcode.com/problems/merge-sorted-array/)\*\*\*\*

### **1.3 Code**

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int first = 0; int last = 0;
        int[] res = new int[m + n];
        int index = 0;
        while(first < m && last < n){
            if(nums1[first] <= nums2[last]){
                res[index] = nums1[first];
                index++;
                first++;
            }
            else{
                res[index] = nums2[last];
                index++;
                last++;
            }
        }
        
        while(first < m){
            res[index] = nums1[first];
            index++;
            first++;
        }
        
        while(last < n){
            res[index] = nums2[last];
            index++;
            last++;
        }
        
        for(int i = 0; i < res.length; i++){
            nums1[i] = res[i];
        }
    }
}
```

## 2. Merge Sort

### 2.1 题目

### [https://leetcode.com/problems/sort-an-array/](https://leetcode.com/problems/sort-an-array/)

Given an array of integers `nums`, sort the array in ascending order.

**Example 1:**

```text
Input: nums = [5,2,3,1]
Output: [1,2,3,5]
```

**Example 2:**

```text
Input: nums = [5,1,1,2,0,0]
Output: [0,0,1,1,2,5]
```

### 2.2 Code

```java
class Solution {
    public int[] sortArray(int[] nums) {
        mergeSort(nums, 0, nums.length - 1);
        return nums;
    }
    
    public void merge(int[] nums, int left, int right, int mid){
        int first = left;
        int last = mid + 1;
        int[] temp = new int[nums.length];
        int index = left;
        int cindex = left;
        while(first <= mid && last <= right){
            if(nums[first] <= nums[last]){
                temp[index] = nums[first];
                first++;
                index++;
            }
            else {
                temp[index] = nums[last];
                index++;
                last++;
            }
        }
        
        while(first <= mid){
            temp[index] = nums[first];
            first++;
            index++;
        }
        
        while(last <= right){
            temp[index] = nums[last];
            index++;
            last++;
        }
        
        //copy back to nums array
        while(cindex <= right){
            nums[cindex] = temp[cindex];
            cindex++;
        }
        
    }
    
    public void mergeSort(int[] nums, int left, int right){
        if(left >= right) return;
        
        int mid = left + (right - left) / 2;
        mergeSort(nums, left, mid);
        mergeSort(nums, mid + 1, right);
        merge(nums, left, right, mid);
    }
}
```

