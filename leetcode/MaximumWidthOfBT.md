```java
    public int widthOfBinaryTree(TreeNode root) {
        int width = 0;
        Queue<Pair<TreeNode, Integer>> q = new LinkedList<>();
        q.offer(new Pair(root,0));
        while(!q.isEmpty()){
                int size = q.size();
                int mini = q.peek().getValue();
                int first, last;
                for(int i=0;i<size;i++){
                    TreeNode curr = q.peek().getKey();
                    int index = q.peek().getValue() - mini;
                    q.poll();
                    if(i == 0) first = index;
                    if(i == size - 1) last = index;
                    if(curr.left != null){
                        q.offer(new Pair(curr.left,  index*2 + 1));
                    }
                    if(curr.right != null){
                        q.offer(new Pair(curr.right,  index*2 + 2));
                    }
                }
             width = Math.max(width, last - first + 1);
               
        }
      return width;
    }
```    
