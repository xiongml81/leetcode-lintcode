# 1. Two Sum

[https://leetcode.com/problems/two-sum/](https://leetcode.com/problems/two-sum/)

  
Solution 1: Two Pointer 

T: O\(nlogn\), S: O\(n\)

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
     
        int[] copy = Arrays.copyOf(nums, nums.length);
        int left = 0; int right = nums.length - 1;
        
        Arrays.sort(nums);
        int[] res = new int[2];
        while(left < right){
            if(nums[left] + nums[right] == target){
                break;
            }
            else if(nums[left] + nums[right] < target){
                left++;
            }
            else {
                right--;
            }
        }
        
        for(int i = 0; i < copy.length; i++){
            if(copy[i] == nums[left]){
                res[0] = i;
            }
            
        }
       
        for(int i = 0; i < copy.length; i++){
             if(copy[i] == nums[right] && i != res[0]){
                res[1] = i;
            }
        }
        
        return res;
    }
}
```

Solution 2: HashMap  
  
T: O\(n\), S:O\(n\)

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> map = new HashMap<>();
        
       
        int[] res = new int[2];
        
        for(int i = 0; i < nums.length; i++){
            int value = target - nums[i];
            if(map.containsKey(value)){
                res[0] = i;
                res[1] = map.get(value);
            }
            
            map.put(nums[i], i);
            
        }
        return res;
    }
}
```

