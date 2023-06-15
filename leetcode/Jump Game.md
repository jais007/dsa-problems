* Solution 1: DP
* Time Complexity : O(N^2)
* Space Complexity : O(N)

```java
    public static boolean canReach(int[] nums, int idx, int []dp) {
        if (idx >= nums.length - 1) {
            return true;
        }
        if(dp[idx] != -1) {
            return dp[idx] == 1;
        }
        for (int i = nums[idx]; i > 0; i--) {
            if (canReach(nums, idx + i,dp)){
               dp[idx] = 1;
               return true;
            }
        }
        dp[idx] = 0;
        return false;
    }
    public boolean canJump(int[] nums) {
        int n = nums.length;
        if(n < 2) return true;
   
        int []dp = new int[nums.length];
        Arrays.fill(dp,-1);
        return canReach(nums,0,dp);
    }
```

* Solution 2: Greedy
* Time Complexity : O(N)
* Space Complexity : O(1)


```java
 public boolean canJump(int[] nums) {
        int n = nums.length;
        if(n < 2) return true;
        int canReach = 0;
        for(int i=0; i<=canReach;i++){
            if(i == n-1){
                return true;
            }
            canReach = Math.max(canReach, nums[i] + i);
        }
        return false;
    }
```