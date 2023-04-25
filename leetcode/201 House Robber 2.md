```cpp
 int houseRobber(vector<int>& nums) {
        // dynamic programming - decide each problem by its sub-problems:
        int dp[nums.size()+1];
        dp[0] = nums[0];
        dp[1] = max(nums[0], nums[1]);
        for (int i=2; i<nums.size(); i++)
            dp[i] = max(dp[i-1], nums[i]+dp[i-2]);
        return dp[nums.size()-1];
    }
    
    int rob(vector<int>& nums) {
        // edge cases:
        if (nums.size() == 0) return 0;
        if (nums.size() == 1) return nums[0];
        if (nums.size() == 2) return max(nums[0], nums[1]);
        
        // either use first house and can't use last or last and not first:
        vector<int> v1(nums.begin(), nums.end()-1);
        vector<int> v2(nums.begin()+1, nums.end());
        return max(houseRobber(v1), houseRobber(v2));
    }
    ```

* Space Optimized
    ```java

      public int rob(int[] nums) {
        if (nums.length == 1) return nums[0];
        return Math.max(rob(nums, 0, nums.length - 2), rob(nums, 1, nums.length - 1));
    }
    private int rob(int[] num, int lo, int hi) {
        int include = 0, exclude = 0;
        for (int j = lo; j <= hi; j++) {
            int i = include, e = exclude;
            include = e + num[j];
            exclude = Math.max(e, i);
        }
        return Math.max(include, exclude);
    }
}
```