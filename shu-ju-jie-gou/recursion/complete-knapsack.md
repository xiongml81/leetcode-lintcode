# Complete Knapsack

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



