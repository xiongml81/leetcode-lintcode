# Counting Sort 计算排序

[https://leetcode.com/problems/sort-colors/](https://leetcode.com/problems/sort-colors/)  
  


```java
class Solution {
    public void sortColors(int[] nums) {
        int[] bucket = new int[3];
        for(int i = 0; i < nums.length; i++){
            bucket[nums[i]]++;
        }
        
        int index = 0;
        for(int i = 0; i < 3; i++){
            while(bucket[i] > 0){
                nums[index] = i;
                index++;
                bucket[i]--;
            }
        }
    }
}
```

  


