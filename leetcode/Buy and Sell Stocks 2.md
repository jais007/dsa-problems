* Buy and Sell Stocks 2 : (Max profit with unlimited) -  Solution 1 (DP) Memoization
time : O(N)
space : O(N)

```java

static int maxProfit(int[] prices) { 
        int n = prices.length;
        int[][] dp = new int[n][2];
        for(int[] row:dp)
           Arrays.fill(row,-1);
        return findMaximumProfit(0, 1, prices, dp);
    }
    static int findMaximumProfit( int i, int k, int[] prices, int[][] dp)
    {
        if(i == prices.length) return 0;
        if(dp[i][k] != -1) return dp[i][k];
        int profit = 0;
        if(k == 1){
            int buy = -prices[i] + findMaximumProfit(i+1,0,prices,dp);
            int notBuy = findMaximumProfit(i+1,1,prices,dp);
            profit = Math.max(buy,notBuy);
        }else{
            int sell = prices[i] + findMaximumProfit(i+1,1,prices,dp);
            int notSell = findMaximumProfit(i+1,0,prices,dp);
            profit = Math.max(sell, notSell);
        }
        return dp[i][k] = profit;
    }
```
DP : Tabulation
```java
long getMaximumProfit(long *Arr, int n)
{
    //Write your code here
    
    vector<vector<long>> dp(n+1,vector<long>(2,-1));
    
    //base condition
    dp[n][0] = dp[n][1] = 0;
    
    long profit;
    
    for(int ind= n-1; ind>=0; ind--){
        for(int buy=0; buy<=1; buy++){
            if(buy==0){// We can buy the stock
                profit = max(0+dp[ind+1][0], -Arr[ind] + dp[ind+1][1]);
            }
    
            if(buy==1){// We can sell the stock
                profit = max(0+dp[ind+1][1], Arr[ind] + dp[ind+1][0]);
            }
            
            dp[ind][buy]  = profit;
        }
    }
    return dp[0][0];
}
```

* Buy and Sell Stocks 2 : (Max profit with unlimited) -  Solution 2 (Greedy)
time : O(N)
space : O(1)

```java
public int maxProfit(int[] prices) {
        int i = 0, buy, sell, profit = 0, N = prices.length - 1;
        while (i < N) {
            while (i < N && prices[i + 1] <= prices[i]) i++;
            buy = prices[i];

            while (i < N && prices[i + 1] > prices[i]) i++;
            sell = prices[i];

            profit += sell - buy;
        }
        return profit;
}
time : O(N)
space : O(1)

```java
int maxProfit(vector<int>& prices) {
        int profit=0;
        for(int i=1;i<prices.size();i++){
            if(prices[i] > prices[i-1]){
                profit+=prices[i]-prices[i-1];
            }
        }
        return profit;
    }


```
