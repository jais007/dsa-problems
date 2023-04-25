```cpp
public:
    void checkTree(TreeNode* root){
        if(!root) return;
        checkTree(root->left);
        if(prev != nullptr && root->val < prev->val){
            //first  violation 
            if(!first){
                first = prev;
                middle = root;
            }
           else{
             //second violation
             last = root;
           }
        }
        prev = root;
        checkTree(root->right);
    }

    void recoverTree(TreeNode* root) {
        if(!root) return;
        first = middle = last = prev = NULL;
        checkTree(root);
        if(!first) return;
        if(first && last){
            swap(first->val,last->val); 
        }
        else if(first && middle){
           swap(first->val,middle->val); 
        }
    }
```