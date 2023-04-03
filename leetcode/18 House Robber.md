### House Robber


```cpp
    int solve(vector<int> &nums, int idx, vector<int> &dp){
        if(idx >= nums.size()) return 0;
        if(dp[idx]!= -1) return dp[idx];
        int rob =  nums[idx] + solve(nums, idx + 2, dp);
        int skip = 0 +  solve(nums, idx + 1, dp);
        return dp[idx] = max(skip, rob);
    }
    int rob(vector<int>& nums) {
        vector<int> dp(nums.size() + 1, -1);
        return solve(nums, 0, dp);
    }
```

```cpp
 int rob(vector<int>& nums) {
        if(nums.size() == 1){
            return nums[0];
        }
        vector<int> dp(nums.size() + 1, -1);
        dp[0] = nums[0];
        dp[1] = max(nums[1], dp[0]);
        for(int i=2; i<nums.size();i++){
            dp[i] = max(dp[i-2] + nums[i], dp[i-1]);
        }
        return dp[nums.size() - 1];
    }
```