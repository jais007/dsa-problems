## Insert Interval in sorted interval

```cpp
 vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
      vector<vector<int>> res;
      if(intervals.size()==0){
          res.push_back(newInterval);
          return res;
      }
      int start= newInterval[0];
      int end=newInterval[1];
      for(int i=0;i<intervals.size();i++){
          
          //case 1 non overlap
          if(intervals[i][1] < start){
              res.push_back({intervals[i][0],intervals[i][1]});
          }
          //case 2 non overlap
          else if(intervals[i][0] > end){
              if(start !=-1 && end !=-1){
                  res.push_back({start,end});
                  start=-1;
                  end=-1;
              }
              res.push_back({intervals[i][0],intervals[i][1]});
          }
          //case 3 overlap
          else {
              start=min(start,intervals[i][0]);
              end=max(end,intervals[i][1]);
          }
      }
        if(start !=-1 && end !=-1){
                  res.push_back({start,end});
                  start=-1;
                  end=-1;
         }
      return res;
    }
```