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

{% embed url="https://labuladong.github.io/algo/3/25/82" %}

DFS:

```java
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

```java
int knapsack(int W, int N, int[] wt, int[] val) {
    // base case 已初始化
    int[][] dp = new int[N + 1][W + 1];
    for (int i = 1; i <= N; i++) {
        for (int w = 1; w <= W; w++) {
            if (w - wt[i - 1] < 0) {
                // 这种情况下只能选择不装入背包
                dp[i][w] = dp[i - 1][w];
            } else {
                // 装入或者不装入背包，择优
                dp[i][w] = Math.max(
                    dp[i - 1][w - wt[i-1]] + val[i-1], 
                    dp[i - 1][w]
                );
            }
        }
    }
    
    return dp[N][W];
}
```

```java
//  Given weights and values of n items, put these items in a knapsack of capacity W to get the maximum total value in the knapsack. 

//       weight  value
// item0  1        15
// item1  3        20
// item2  4        30


public static void testWeightBagProblem(int[] weight, int[] value, int bagWeight){
        int wLen = weight.length;
        //定义dp数组：dp[j]表示背包容量为j时，能获得的最大价值
        int[] dp = new int[bagWeight + 1];
        //遍历顺序：先遍历物品，再遍历背包容量
        for (int i = 0; i < wLen; i++){
            for (int j = bagWeight; j >= weight[i]; j--){
                dp[j] = Math.max(dp[j], dp[j - weight[i]] + value[i]);
            }
        }
        //打印dp数组
        for (int j = 0; j <= bagWeight; j++){
            System.out.print(dp[j] + " ");
        }
    }
```
