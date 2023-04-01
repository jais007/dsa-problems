### Merge Intervals

```cpp
    bool static comp(vector<int> &a, vector<int> &b){
        if(a[0] == b[0]){
            return a[1] < b[1];
        }
        return a[0] < b[0];
    }
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        sort(intervals.begin(),intervals.end(), comp);
        vector<vector<int>> merged;
        int start = -1;
        int end = -1;
        for(int i=0; i < intervals.size(); i++){
            if(start == -1 && end ==-1){
                start = intervals[i][0];
                end = intervals[i][1];
            }
            if(i + 1 < intervals.size() && intervals[i+1][0] <= end){
                start = min(intervals[i+1][0],start);
                end = max(intervals[i+1][1],end);
            }else{
                merged.push_back({start,end});
                start = end = -1;
            }
        }
        return merged;
    }
```