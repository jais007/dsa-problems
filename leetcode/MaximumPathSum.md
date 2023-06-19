```java
private int solve(TreeNode root, int[] maxSum){
        if(root == null) return 0;

        int leftSum =  Math.max(0, solve(root.left, maxSum));
        int rightSum = Math.max(0, solve(root.right, maxSum));

        maxSum[0] =Math.max(maxSum[0], leftSum + rightSum + root.val);
        return Math.max(leftSum, rightSum) + root.val;

    }
    public int maxPathSum(TreeNode root) {
        int maxSum[] = new int[1];
        maxSum[0] = Integer.MIN_VALUE;
        solve(root, maxSum);
        return maxSum[0];
    }
```
