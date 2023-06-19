```java
  
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> post = new ArrayList<>(); 
        Stack<Pair<TreeNode, Integer>> S = new Stack<>();
        TreeNode curr = root;
        S.push(new Pair(root, 0));
        while(!S.isEmpty()){
            TreeNode cur = S.peek().getKey();
            int state = S.peek().getValue();
            S.pop();

            if(cur == null || state == 3) 
                continue;
            S.push(new Pair(cur, state + 1));

            if(state == 0) 
                S.push(new Pair(cur.left, 0));
            else if(state ==1) 
                S.push(new Pair(cur.right, 0));
            else if(state == 2)
                post.add(cur.val);
        }
        return post;
    } 
```    
    
