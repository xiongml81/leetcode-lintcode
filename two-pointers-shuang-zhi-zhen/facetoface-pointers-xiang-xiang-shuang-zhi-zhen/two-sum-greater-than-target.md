# 443. Two Sum - Greater than target

[https://www.lintcode.com/problem/two-sum-greater-than-target/description](https://www.lintcode.com/problem/two-sum-greater-than-target/description)



```java
public class Solution {
    /**
     * @param nums: an array of integer
     * @param target: An integer
     * @return: an integer
     */
    public int twoSum2(int[] nums, int target) {
        // write your code here
        
        Arrays.sort(nums);
        int left = 0; int right = nums.length - 1;
        int count = 0;
        while(left < right){
            if(nums[left] + nums[right] <= target){
                left++;
            }
            else{
                count+= right - left;
                right--;
            }
        }
        return count;
    }
}
```

