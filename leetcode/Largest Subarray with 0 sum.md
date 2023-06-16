

Intuition : 
 
   <----------S------------->
   <--S--->|<-------0------->
```java
    int maxLen(int arr[], int n){
        Map<Integer, Integer> map = new HashMap<>();
        int currSum = 0;
        int maxi = 0;
        for(int i=0; i < n; i++){
            currSum += arr[i];
            
            if(currSum == 0){
                maxi = Math.max(maxi, i + 1); 
            }
            
            if(!map.containsKey(currSum)){
                map.put(currSum, i);
            }else{
                maxi = Math.max(maxi, i - map.get(currSum));
            }
        }
        return maxi;
    }
```    