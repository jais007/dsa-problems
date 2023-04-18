# Num of way to make change with given coins

https://leetcode.com/problems/coin-change-ii/submissions/
You are given an integer array coins representing coins of different denominations and an integer amount representing a total amount of money.

Return the number of combinations that make up that amount. If that amount of money cannot be made up by any combination of the coins, return 0.

You may assume that you have an infinite number of each kind of coin.

The answer is guaranteed to fit into a signed 32-bit integer.

 

Example 1:

Input: amount = 5, coins = [1,2,5]
Output: 4
Explanation: there are four ways to make up the amount:
5=5
5=2+2+1
5=2+1+1+1
5=1+1+1+1+1

```java
    private int CoinChangeHelper(int[] coins, int sum, int idx, int [][]dp){
      if(idx == coins.length || sum < 0){
         return 0;
      }
      if(sum == 0){
         return 1;
      }
      if(dp[sum][idx] != -1){
           return dp[sum][idx];
      }
      int takeIt = CoinChangeHelper(coins, sum - coins[idx], idx, dp);
      int skipIt = CoinChangeHelper(coins, sum, idx + 1, dp);
      return dp[sum][idx] = takeIt + skipIt;
  }
    public int change(int sum, int[] coins) {
        if(sum == 0) return 1;
        if(coins == null || coins.length == 0) return 0;
        int n = coins.length;
        int [][]dp = new int[sum + 1][n + 1];
        for(int []row : dp)
            Arrays.fill(row, -1);
        return CoinChangeHelper(coins, sum , 0, dp);
    }
```