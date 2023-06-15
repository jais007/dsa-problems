```cpp
 int maxArea(vector<int>& A) {
        int maxi = -1;
        int w = A.size() - 1;
        int i=0;
        int j=A.size() -1;
        while(i < j){
            maxi = max(maxi, min(A[i], A[j]) * w);
            if(A[i] <= A[j]){
                i++;
            }else{
                j--;
            }
            w--;
        }
        return maxi;
    }

```