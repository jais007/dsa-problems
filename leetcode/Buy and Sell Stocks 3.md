* Buy and Sell Stocks 3 : (Max profit with at max 2 transection)

https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/solutions/135704/detail-explanation-of-dp-solution/?orderBy=most_votes

```cpp
   int maxProfit(vector<int>& prices) {
        int n=prices.size();
        if(n==0||n==1) return 0;
        vector<vector<int>> profit(3,vector<int>(n,0));
        int k=2;
        for(int t=1;t<=k;t++){
            int maxThusFar=INT_MIN;
              for(int d=1;d<n;d++){
                maxThusFar=max(maxThusFar,profit[t-1][d-1]-prices[d-1]);
                profit[t][d]=max(profit[t][d-1],maxThusFar+prices[d]);
            }
        }
      return profit[k][n-1];
    }
```