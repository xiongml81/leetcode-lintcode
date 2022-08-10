# Complete Knapsack 背包问题

// Given weights and values of n items, put these items in a knapsack of capacity W to get the maximum total value in the knapsack.

// Each item can choose multiple times.

```java

// Example:


//        weight  value
//  item0  1        15
//  item1  3        20
//  item2  4        30

private static int process(int[] weights, int[] values, int capacity){
    int[][] dp = new int[weights.length + 1][capacity + 1];

    for(int i = 1; i <= weights.length; i++){
      for(int j = 1; j <= capacity; j++){
        if(weights[i - 1] > j){
          dp[i][j] = dp[i - 1][j];
        }
        else {
          //未优化
          // for(int k = 0; k * weights[i -1] <= j; k++){
          //   int temp = dp[i- 1][j - k*weights[i-1]] + k*values[i - 1];
          //   if(temp > dp[i][j]){
          //     dp[i][j] = temp;
          //   }
            
          // }
         
          dp[i][j] =    Math.max(dp[i-1][j],dp[i][j-weights[i -1]] + values[i - 1]);
        }
      }
    }

    return dp[weights.length][capacity];
  }
```

\
\
递推关系：&#x20;

dp\[0]\[j]=0

dp\[i+1]\[j]=max{dp\[i]\[j-k_w\[i]]+k_v\[i]|0<=k}

但直接这样去写程序是三重循环，时间复杂度为O(mW^2).

在这个算法中有多余的计算：

在dp\[i+1]\[j]的计算中选择k(k>=1)个 i 物品的情况，与在dp\[i+1]\[j-w\[i]]的计算中选择k-1的情况是相同的，所以dp\[i+1]\[j]的递推中k>=1部分的计算已经在dp\[i+1]\[j-w\[i]]的计算中完成了。那么可以按照如下方式进行变形：

dp\[i+1]\[j]

\=max{dp\[i]\[j-k_w\[i]]+k_v\[i]|0<=k}

\=max(dp\[i]\[j],max{dp\[i]\[j-k_w\[i]]+k_v\[i]|1<=k})

\=max(dp\[i]\[j],max{dp\[i]\[(j-w\[i])-k_w\[i]]+k_v\[i]|0<=k}+v\[i])

\=max(dp\[i]\[j],dp\[i+1]\[j-w\[i]]+v\[i])

这样一来就可以用O(nW)时间解决问题。



**一维DP:**

```java
  private static int process2(int[] weights, int[] values, int capacity){
    int[] dp = new int[capacity + 1];

    for(int i = 0; i < weights.length; i++){
      for(int j = weights[i]; j <= capacity; j++){
        dp[j] = Math.max(dp[j], dp[j - weights[i]] + values[i]);
      }
    }

    return dp[capacity];
  }
```
