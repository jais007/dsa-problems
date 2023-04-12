```java
 private boolean solve(int[] nums, int idx, int target, int[][] dp){
        if(idx < 0 || target < 0) return false;
        if(target == 0) return true;
        if(dp[idx][target] != -1 ) {
            return dp[idx][target] == 1 ? true : false ;
        }
        boolean takeIt = solve(nums, idx - 1, target - nums[idx], dp);
        boolean skipIt = solve(nums, idx - 1, target, dp);
        int result = 0;
        if(takeIt || skipIt){
            result = 1;
        }
        dp[idx][target] = result; 
        return takeIt || skipIt;
    }
    public boolean canPartition(int[] nums) {
        int sum = 0;
        for(int i=0;i<nums.length;i++) sum+=nums[i];
        if(sum % 2 != 0) return false;
        int [][]dp = new int[nums.length][sum/2 + 1];
        for (int[] row : dp)
            Arrays.fill(row, -1);
        return solve(nums, nums.length - 1, sum/2, dp);
    }
    ```