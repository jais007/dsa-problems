```cpp
class Solution {
public:

    TreeNode* solve(vector<int>& inorder, vector<int>& postorder, int inStart, int inEnd, int &index) {
        if(inStart > inEnd) 
              return nullptr;
        TreeNode* root = new TreeNode(postorder[index]);
        int i=0;
        for(;i<inorder.size();i++){
            if(postorder[index] == inorder[i]){
              break;
            }
        }
        index-=1;
        root->right =solve(inorder, postorder, i + 1, inEnd, index);
        root->left = solve(inorder, postorder, inStart, i - 1, index);
        return root;
    }
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        if(inorder.size()==0 && postorder.size()==0) return nullptr;
        int index = inorder.size() - 1;
        return solve(inorder, postorder, 0, inorder.size() -1, index);
    }
};
```