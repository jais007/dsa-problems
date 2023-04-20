

*
```java

int trap(vector<int>& height) {
        if(height.size()==0) return 0;
        int n=height.size();
        vector<int> left(n);
        vector<int> right(n);
        left[0]=height[0];
        right[n-1]=height[n-1];
        for(int i=1;i<n;i++)
        {
            left[i]=max(left[i-1],height[i]);
        }
        for(int i=n-2;i>=0;i--)
        {
            right[i]=max(right[i+1],height[i]);
        }
        int sum=0;
        for(int i=0;i<n;i++)
        {
            sum+=min(left[i],right[i])-height[i];
        }
        return sum;
    }


```

* Space : O(1)


```java

 int trap(vector<int>& height) {
        if(height.size()==0) return 0;
        int n=height.size();
        int L=0, R=n-1;
        int lmax=-1,rmax=-1;
        int water=0;
        
        while(L < R){
            if(height[L] <= height[R]){
                 if(height[L] >=lmax){
                     lmax=height[L];
                 }else{
                     water+=lmax-height[L];
                 }
                L++;
            }else{
                if(height[R] >=rmax){
                    rmax=height[R];
                }else{
                    water+=rmax-height[R];
                }
                R--;
            }
        }
      return water;
    }
```