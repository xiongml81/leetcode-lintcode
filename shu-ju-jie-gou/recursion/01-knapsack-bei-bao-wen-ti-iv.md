# 0-1 Knapsack 背包问题 IV

Given a knapsack which can hold s pounds of items, and a set of items with weight w1, w2, ... wn. Try to put items into the pack as many as possible, return the largest weight we can get in the knapsack.\
\


```java
public static int knapsack5(int target, int[] items, int index){
		if(target == 0 || index == items.length){
			return 0;
		}

		if(items[index] > target){
			return knapsack5(target, items, index + 1);
		}

		return Math.max(knapsack5(target, items, index + 1),
				items[index] + knapsack5(target - items[index], items, index + 1));
	}
```
