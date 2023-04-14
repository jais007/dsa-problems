* Solution 1 : DP 
* Time Complexity : O(N^2)
* Space Complexity : O(N)
```java
    public int minimumJump(int []nums, int []dp, int idx, int n){
        if(idx >= n) {
            return 0;
        }
       if(dp[idx] != -1) return dp[idx];
       int mini = Integer.MAX_VALUE;
        for(int j =  nums[idx]; j > 0 ; j--){
		      mini = Math.min(mini, 1 + minimumJump(nums, dp, idx + j, n));       
        }
        return dp[idx] = mini == Integer.MAX_VALUE ? Integer.MAX_VALUE - 1 : mini;
    }
    public int jump(int[] nums) {
        int n = nums.length;
        if(n < 2) return 0;
        int []dp = new int[n];
        Arrays.fill(dp,-1);
        return minimumJump(nums,dp,0,n - 1);
    }
```

* Solution 2 : Greedy 
* Time Complexity : O(N)
* Space Complexity : O(1)
```java
    public int jump(int[] nums) {
        int n = nums.length;
        if(n < 2) return 0;
        int target = n-1;
        int jump = 0;
        while(target != 0){
            for(int i=0;i<=target;i++){
                if(nums[i] + i >= target){
                    target = i;
                    break;
                }
            }
            jump++;
        }
        return jump;

    }
```