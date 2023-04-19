* Prioriry Queue. : N * log(K)
```java
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        /*
         left = 0
         right = 2
          PQ = [ (1,0), (3, 1), (-1, 2)]
          ans = []
        */
        vector<int> ans;
        priority_queue<pair<int,int>> pq; // element , index
        int left = 0, right = 0;
        while( right < nums.size()){

            // add element in PQ;
            pq.push({nums[right], right});
            //if windows size is not full 
            if(right - left + 1 < k){
                    right++;
            // window is full
            }else{
                 
                 //remove invalid element from window
                while(pq.top().second < left){
                     pq.pop();
                 }
                ans.push_back(pq.top().first);
                left++;
                right++;
            }
        }
        return ans;

    }
```



* Using Deque : O(N)

```java
 vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        deque<int> dq;
        int n=nums.size();
        vector<int> ans;
        int i;
        for(i=0;i<k;i++){
            while(!dq.empty() && nums[i] > nums[dq.back()]){
                dq.pop_back();
            }
            dq.push_back(i);
        }
        for(;i<n;i++){
             
             ans.push_back(nums[dq.front()]);
             while(!dq.empty() && nums[i] > nums[dq.back()]){
                dq.pop_back();
            }
            while(!dq.empty() && i-dq.front()>= k){
                dq.pop_front();
            }
            dq.push_back(i);
        }
        ans.push_back(nums[dq.front()]);
        return ans;
    }
```