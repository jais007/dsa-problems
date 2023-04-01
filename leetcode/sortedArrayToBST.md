 ### Sorted Array To BST

```java
 private TreeNode buildTree(int l, int r, int[] nums){
        if(l > r){
            return null;
        }
        int mid = l + (r - l)/2;
        TreeNode root = new TreeNode(nums[mid]);
        root.left = buildTree(l, mid - 1, nums);
        root.right = buildTree(mid + 1, r, nums);
        return root;
    }
    public TreeNode sortedArrayToBST(int[] nums) {
        if(nums == null || nums.length == 0) return null;
        int left = 0, right = nums.length - 1;
        return buildTree(left, right, nums);
    }
```
