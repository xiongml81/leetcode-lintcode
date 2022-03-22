# 0-1 Knapsack (DP)

0-1 Knapsack Given a knapsack which can hold w pounds of items, and a set of items with weight w1, w2, ... wn. Each item has its value s1,s2,...,sn. Try to select the items that could put in knapsack and contains most value.

给你一个可装载重量为 `W` 的背包和 `N` 个物品，每个物品有重量和价值两个属性。其中第 `i` 个物品的重量为 `wt[i]`，价值为 `val[i]`，现在让你用这个背包装物品，最多能装的价值是多少？

举个简单的例子，输入如下：

```
N = 3, W = 4
wt = [2, 1, 3]
val = [4, 2, 3]
```

算法返回 6，选择前两件物品装进背包，总重量 3 小于 `W`，可以获得最大价值 6。



DFS:

```
public static void knapsack(int index, int sumw, int sumv, int s, int[] weights, int[] values){
		if(index == weights.length){
			if(sumw <= s){
				if(sumv  > maxValue){
					maxValue = sumv;
				}
			}
			return;
		}

		knapsack(index + 1, sumw, sumv, s, weights, values); // not choose

		knapsack(index + 1, sumw + weights[index], sumv + values[index], s, weights, values); //  choose


	}
```
