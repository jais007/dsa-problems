```cpp
class Solution {
public:
    int solve(vector<int> &nums,int start, int idx, vector<int> &dp){
        if(idx < start) return 0;
        if(idx == start) return nums[start];
        if(dp[idx]!= -1) 
            return dp[idx];
        int rob =  nums[idx] + solve(nums, start, idx - 2, dp);
        int skip = 0 +  solve(nums, start, idx - 1, dp);
        return dp[idx] = max(skip, rob);
    }
    int rob(vector<int>& nums) {
        if(nums.size() == 0) return 0;
        if(nums.size() == 1) return nums[0];
        vector<int> dp(nums.size() + 1, -1);
        vector<int> dp2(nums.size() + 1, -1);
        int ans1 = solve(nums, 1, nums.size() - 1, dp);
         //dp.resize(nums.size() + 1, -1);
        int ans2 = solve(nums, 0, nums.size() - 2 , dp2);
        return max(ans1,ans2);
    }
};
```