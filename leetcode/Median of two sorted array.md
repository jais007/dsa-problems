* Intuition :

We came up with a naive solution because of the hint that two arrays are sorted and we want elements from merged sorted arrays. If we look into the word “sorted arrays”, we can think of a binary solution. Hence, we move to an efficient solution using binary search. But how to apply binary search? Let’s look into the thought process.

We know that we will get answers only from the final merged sorted arrays. We figured it out with the naive approach discussed above. We will partition both the arrays in such a way that the left half of the partition will contain elements, which will be there when we merge them, till the median element and rest in the other right half. This partitioning of both arrays will be done by binary search.

* Approach :

We will do a binary search in one of the arrays which have a minimum size among the two. 

Firstly, calculate the median position with (n+1)/2. Point two-pointer, say low and high, equal to 0 and size of the array on which we are applying binary search respectively. Find the partition of the array. Check if the left half has a total number of elements equal to the median position. If not, get the remaining elements from the second array. Now, check if partitioning is valid. This is only when l1<=r2 and l2<=r1. If valid, return max(l1,l2)(when odd number of elements present) else return (max(l1,l2)+min(r1,r2))/2.

If partitioning is not valid, move ranges. When l1>r2, move left and perform the above operations again. When l2>r2, move right and perform the above operations.

```java
static double median(int arr1[],int arr2[],int m,int n) {
    if(m>n)
        return median(arr2,arr1,n,m);//ensuring that binary search happens on minimum size array
        
    int low=0,high=m,medianPos=((m+n)+1)/2;
    while(low<=high) {
        int cut1 = (low+high)>>1;
        int cut2 = medianPos - cut1;
        
        int l1 = (cut1 == 0)? Integer.MIN_VALUE:arr1[cut1-1];
        int l2 = (cut2 == 0)? Integer.MIN_VALUE:arr2[cut2-1];
        int r1 = (cut1 == m)? Integer.MAX_VALUE:arr1[cut1];
        int r2 = (cut2 == n)? Integer.MAX_VALUE:arr2[cut2];
        
        if(l1<=r2 && l2<=r1) {
            if((m+n)%2 != 0)
                return Math.max(l1,l2);
            else 
                return (Math.max(l1,l2)+Math.min(r1,r2))/2.0;
        }
        else if(l1>r2) high = cut1-1;
        else low = cut1+1;
    }
    return 0.0;
}
```

* Time Complexity : O(log(min(m,n)))

Reason – We are applying binary search on the array which has a minimum size.

* Space Complexity: O(1)
