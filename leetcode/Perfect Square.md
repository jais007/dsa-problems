```cpp
 int findNumSquares(vector<int> &arr,int i,int sum,vector<int>&dp){
        if(i==arr.size()) {
            return INF;
        }
        if(sum==0){
            return 0;
        }
        if(dp[sum]!=0){
            return dp[sum];
        }
        if(sum-arr[i] >=0){
            int incl=1+findNumSquares(arr,i,sum-arr[i],dp);
            int excl=findNumSquares(arr,i+1,sum,dp);
             return dp[sum]=min(incl,excl);
        }
        return INF;
          
    }
    int numSquares(int n) {
        vector<int> arr;
        arr.push_back(1);
        for(int i=2;i*i<=n;i++){
            arr.push_back(i*i);
        }
        vector<int> dp(n+1,0);
        return findNumSquares(arr,0,n,dp);
    }
```