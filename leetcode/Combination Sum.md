### Combination Sum
```cpp

   void solve(int target, vector<int>& candidates, vector<vector<int>> &ans, vector<int> &temp, int idx){
            if(idx == candidates.size() || target < 0 ) return;
            if(target == 0){
                ans.push_back(temp);
                return;
            }
            for(int i = idx ; i<candidates.size();i++){
                temp.push_back(candidates[i]);
                solve(target - candidates[i], candidates, ans, temp, i);
                temp.pop_back();
            }
    }

    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        vector<vector<int>> ans;
        vector<int> temp;
        solve(target, candidates, ans, temp, 0);
        return ans;
    }
    
```