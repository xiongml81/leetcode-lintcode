# 0-1 Knapsack 背包问题 III

Given a collection of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.&#x20;

Candidate numbers may contain duplicate.

&#x20;Each number in C may only be used once in the combination.\
\
方法1： 根据上一问题代码，加去重即可



方法2：

```java
public static void knapsack3(int[] items, ArrayList<ArrayList<Integer>> result,
								 ArrayList<Integer> cur, int index, int target){
		if(target == 0){
			result.add(new ArrayList<Integer>(cur));
			return;
		}

		if(target < 0 || (items.length == index && target != 0)){
			return;
		}

		for(int i = index; i < items.length; i++){
			cur.add(items[i]);
			knapsack3(items, result, cur, i + 1, target - items[i] );
			cur.remove(cur.size() - 1);
			while( i < items.length - 1 && items[i] == items[i+ 1]) i++; //去重
		}

	}
```
