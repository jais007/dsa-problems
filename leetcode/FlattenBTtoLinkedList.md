```java
class Solution {
  private static Node prev = null;
  public static void flatten(Node root) {
  Node cur = root;
		while (cur!=null){
			if(cur.left!=null){
				Node pre = cur.left;
				while(pre.right!=null){
					pre = pre.right;
				}
				pre.right = cur.right;
				cur.right = cur.left;
				cur.left = null;
			}
			cur = cur.right;
		}
  }
}
```
