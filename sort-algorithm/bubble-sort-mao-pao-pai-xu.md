# Bubble Sort 冒泡排序

相邻两个数两两比较，把大的放右边

Time：Average O\(n^2\), Best O\(n\)

```java
public static void bubblesort(int[] nums) {
		int n = nums.length;
		for(int i = 0; i < nums.length; i++) {
			for(int j = 1; j < (n - i); j++) {
				if(nums[j - 1] > nums[j]) {
					int temp = nums[j];
					nums[j] = nums[j-1];
					nums[j-1] = temp;
				}
			}
		}
	}
```

