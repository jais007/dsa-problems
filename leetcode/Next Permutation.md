### Next Permutation 

* Swap
```java 
 public void swap(int[] A, int i, int j) {
        int tmp = A[i];
        A[i] = A[j];
        A[j] = tmp;
    }

```
* Reverse 
```java
  public void reverse(int[] A, int i, int j) {
        while(i < j) swap(A, i++, j--);
    }

```
```java

    public void nextPermutation(int[] A) {
        if(A == null || A.length <=1) return;
        int n = A.length;

        // Step 1: Find the break point:
        int ind = -1; // break point
        for (int i = n - 2; i >= 0; i--) {
            if (A[i] < A[i+1]) {
                // index i is the break point
                ind = i;
                break;
            }
        }

        // If break point does not exist:
        if (ind == -1) {
            // reverse the whole array:
            reverse(A, 0 ,n - 1);
            return;
        }

        // Step 2: Find the next greater element
        //         and swap it with arr[ind]:

        for (int i = n - 1; i > ind; i--) {
            if (A[i] > A[ind]) {
                swap(A,i,ind);
                break;
            }
        }

        // Step 3: reverse the right half:
        reverse(A, ind + 1, n - 1); 
    }
```