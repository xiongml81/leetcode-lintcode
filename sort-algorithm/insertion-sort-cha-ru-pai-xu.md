# Insertion Sort 插入排序

```java
public static void insertionsort(int[] nums) {
		for(int i = 1; i < nums.length; i++) {
			for(int j = i; j > 0; j--) {
				if(nums[j - 1] > nums[j]) {
					int temp = nums[j];
					nums[j] = nums[j-1];
					nums[j-1] = temp;
				}
			}
		}
	}
```

