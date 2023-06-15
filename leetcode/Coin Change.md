## Minimum Coin needed to make change for given amount

https://leetcode.com/problems/coin-change/submissions/

You are given an integer array coins representing coins of different denominations and an integer amount representing a total amount of money.

Return the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

You may assume that you have an infinite number of each kind of coin.

 

Example 1:

Input: coins = [1,2,5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1

* Solution 1


```java

    int solve(vector<int>& coins, int amount, vector<int> &dp){
        if(amount == 0) return 0;
        if(amount < 0) return INT_MAX;
        if(dp[amount] != -1) return dp[amount];
        int min_coin = INT_MAX;
        for(int i = 0 ; i < coins.size(); i++){
            int ans = solve(coins , amount - coins[i], dp);
            if(ans != INT_MAX){
                  min_coin =  min(min_coin, ans + 1);
            }
        }
        return dp[amount] = min_coin;
    }
    int coinChange(vector<int>& coins, int amount) {
        if(amount == 0) return 0;
        int n = coins.size();
        // vector<vector<int>> dp(n , vector<int>(amount + 1, -1));
        vector<int> dp(amount + 1, -1);
        int min_coin = solve(coins, amount, dp);
        return  min_coin != INT_MAX ? min_coin : -1;
    }
```


* Solution 2


```cpp

   int solve(vector<int>& coins, int idx, int amount, vector<vector<int>> &dp){
        if(idx == 0){
            if(amount % coins[0] == 0) return amount/coins[0];
            return INT_MAX - 1;
        }
        if(amount == 0){
            return 0;
        }
        if(dp[idx][amount] != -1) return dp[idx][amount];
        int doNotTake = 0 + solve(coins, idx - 1, amount - 0, dp);
        int take = INT_MAX;
        if(coins[idx] <= amount){
            take = 1 + solve(coins, idx, amount - coins[idx], dp);
        }
       
        return dp[idx][amount] = min(take, doNotTake);
    }
    int coinChange(vector<int>& coins, int amount) {
        if(amount == 0) return 0;
        int n = coins.size();
        vector<vector<int>> dp(n , vector<int>(amount + 1, -1));
        int res = solve(coins, coins.size() - 1, amount, dp);
        return res >= 1e9 ? -1 : res;
    }
```