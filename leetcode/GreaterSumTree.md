```java

    private void solve(TreeNode root, int totalSum[]){
        if(root == null){
            return;
        }
        if(root.left == null && root.right == null){
            totalSum[0] += root.val;
            root.val = totalSum[0];
            return;
        }
        solve(root.right, totalSum);
        totalSum[0] += root.val;
        root.val = totalSum[0]; 
        solve(root.left, totalSum);
    }
    public TreeNode bstToGst(TreeNode root) {
        if(root == null){
            return null;
        }
        int totalSum[] = new int[1];
        totalSum[0] = 0;
        solve(root, totalSum);
        return root;
    }
```    
