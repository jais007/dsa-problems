```java
void solve(TreeNode root, TreeNode prev){
        if(root == null) return;
        solve(root.right, prev);
        solve(root.left, prev);
        root.right = prev;
        root.left = null;
        prev = root;
    }
    void flatten(TreeNode root) {
        TreeNode prev = null;
        solve(root, prev);
    }
```

* Itereative

  ```java
      public void flatten(TreeNode root) {
        Stack<TreeNode> s = new Stack<>();
        s.push(root);
        TreeNode curr = null;
        while(!s.isEmpty()){
            curr = s.peek();s.pop();
            if(curr == null) continue;
            if(curr.right!=null){
                s.push(curr.right);
            }
            if(curr.left!=null){
                s.push(curr.left);
            }
            if(!s.isEmpty()){
                curr.right = s.peek();
            }
            curr.left = null;
        }
    }
   ``` 
