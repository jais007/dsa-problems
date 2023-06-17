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
* Java Code
* Time Complexity: O(2^t * k) where t is the target, k is the average length

Reason: Assume if you were not allowed to pick a single element multiple times, every element will have a couple of options: pick or not pick which is 2^n different recursion calls, also assuming that the average length of every combination generated is k. (to put length k data structure into another data structure)

Why not (2^n) but (2^t) (where n is the size of an array)?

Assume that there is 1 and the target you want to reach is 10 so 10 times you can “pick or not pick” an element.

* Space Complexity: O(k*x), k is the average length and x is the no. of combinations
  ```java
   private void findCombinations(int ind, int[] arr, int target, List < List < Integer >> ans, List < Integer > ds) {
        if (ind == arr.length) {
            if (target == 0) {
                ans.add(new ArrayList < > (ds));
            }
            return;
        }

        if (arr[ind] <= target) {
            ds.add(arr[ind]);
            findCombinations(ind, arr, target - arr[ind], ans, ds);
            ds.remove(ds.size() - 1);
        }
        findCombinations(ind + 1, arr, target, ans, ds);
    }
    public List < List < Integer >> combinationSum(int[] candidates, int target) {
        List < List < Integer >> ans = new ArrayList < > ();
        findCombinations(0, candidates, target, ans, new ArrayList < > ());
        return ans;
    }
  ```
