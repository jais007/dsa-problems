## 108. Convert Sorted Array to Binary Search Tree

### Question:
Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

```
Example:

Given the sorted array: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5
```

* Method 1: BST + binary search
```Java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode sortedArrayToBST(int[] nums) {
        if(nums == null || nums.length == 0) return null;
        return createTree(nums, 0, nums.length - 1);
    }
    private TreeNode createTree(int[] nums, int start, int end){
        if(start > end) return null;
        int mid = start + (end - start) / 2;
        TreeNode node = new TreeNode(nums[mid]);
        node.left = createTree(nums, start, mid - 1);
        node.right = createTree(nums, mid + 1, end);
        return node;
    }
}
```
