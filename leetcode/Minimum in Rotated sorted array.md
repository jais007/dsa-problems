# Find minimum in rotated sorted array
```java
 int findMin(int arr[], int n){
       int mini = Integer.MAX_VALUE;
       int low = 0, high = n - 1;
       while(low <= high){
           int mid = low + (high - low)/2;
           //if left part is sorted
           if(arr[low] <= arr[mid]){
               mini = Math.min(mini, arr[low]);
               low = mid + 1;
           }
            //if right part is sorted
           else{
              mini = Math.min(mini, arr[mid]);
              high = mid - 1;
           }
       }
    return mini; 
    }
```