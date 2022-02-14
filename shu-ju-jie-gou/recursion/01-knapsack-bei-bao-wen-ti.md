# 0-1 Knapsack 背包问题

Given a knapsack which can hold s pounds of items, and a set of items with weight w1, w2, ... wn. Return whether we can pick specific items so that their total weight s.&#x20;

Example Input: s = 20; w = \[14, 8, 7, 5, 3];&#x20;

Example Output: True;&#x20;

Given an item, just two options: pick it, the problem become (s-w\[i], w - w\[i]) not pick it, the problem become (s, w - w\[i])\
\
思路：&#x20;

\-每个物品两种选择，选或者不选

\-用index作为参数，一个个物品看

\-退出条件，重量最后为零，找到。重量<0，或者index == weight.length, 表示找不到



```java
public static boolean knapsack(int s, int[] weights, int index) {
	if (s == 0) {
		return true;
	}
	if (s < 0 || index == weights.length) {
		return false;
	}
	return knapsack(s - weights[index], weights, index+1) ||
			knapsack(s, weights, index+1);
}
```
