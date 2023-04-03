```cpp
class Solution {
public:
    TreeNode* solve(vector<int>& pre, vector<int>& in, int inStart, int inEnd, int &index) {
          if(inStart > inEnd) return nullptr;
          TreeNode *root = new TreeNode(pre[index]);
          int i=0;
          for(;i<=inEnd;i++){
             if(pre[index] == in[i]){
                 break;
             }
          }
          index += 1;
          root->left = solve(pre, in, inStart, i-1, index);
          root->right = solve(pre, in, i + 1, inEnd, index);
        
        return root;
    }

      TreeNode* buildTree(vector<int>& pre, vector<int>& in) {
          int index = 0;
          return solve(pre, in, 0, in.size()-1, index);
    }
};
```