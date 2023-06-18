```java
    static int kthelement(int arr1[], int arr2[], int m, int n, int k) {
    if(m > n) {
        return kthelement(arr2, arr1, n, m, k); 
    }
        
    int low = Math.max(0,k-m), high = Math.min(k,n);
        
    while(low <= high) {
        int cut1 = (low + high) >> 1; 
        int cut2 = k - cut1; 
        int l1 = cut1 == 0 ? Integer.MIN_VALUE : arr1[cut1 - 1]; 
        int l2 = cut2 == 0 ? Integer.MIN_VALUE : arr2[cut2 - 1];
        int r1 = cut1 == n ? Integer.MAX_VALUE : arr1[cut1]; 
        int r2 = cut2 == m ? Integer.MAX_VALUE : arr2[cut2]; 
            
        if(l1 <= r2 && l2 <= r1) {
            return Math.max(l1, l2);
        }
        else if (l1 > r2) {
            high = cut1 - 1;
        }
        else {
            low = cut1 + 1; 
        }
    }
    return -1;
    }
  ```

Time Complexity : log(min(m,n))

Reason: We are applying binary search in the array with minimum size among the two. And we know the time complexity of the binary search is log(N) where N is the size of the array. Thus, the time complexity of this approach is log(min(m,n)), where m, and n are the sizes of two arrays.

Space Complexity: O(1)
