```java
 public static void merge(long[] arr1, long[] arr2, int n, int m) {

        // Declare 2 pointers:
        int left = n - 1;
        int right = 0;

        // Swap the elements until arr1[left] is
        // smaller than arr2[right]:
        while (left >= 0 && right < m) {
            if (arr1[left] > arr2[right]) {
                long temp = arr1[left];
                arr1[left] = arr2[right];
                arr2[right] = temp;
                left--;
                right++;
            } else {
                break;
            }
        }

        // Sort arr1[] and arr2[] individually:
        Arrays.sort(arr1);
        Arrays.sort(arr2);
    }
```    
