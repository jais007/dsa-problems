```java
    public int merge(int arr[], int low, int mid, int high) {
        int i = low;
        int j = mid;
        int k = 0;
        int count = 0;
        int temp[] = new int[high - low + 1];
        Arrays.fill(temp, 0);
        while (i < mid && j <= high) {
            if (arr[i] > arr[j]) {
                count += mid - i;
                temp[k++] = arr[j++];
            } else {
                temp[k++] = arr[i++];
            }
        }
        while (i < mid) {
            temp[k++] = arr[i++];
        }
        while (j <= high) {
            temp[k++] = arr[j++];
        }

        for (i = low, k = 0; i <= high; i++, k++) {
            arr[i] = temp[k];
        }
        return count;
    }

    public int mergeSort(int arr[], int low, int high) {
        int count = 0;
        if (low < high) {
            int mid = low + (high - low) / 2;
            count += mergeSort(arr, low, mid);
            count += mergeSort(arr, mid + 1, high);
            count += merge(arr, low, mid + 1, high);
        }
        return count;

    }

    public int getInversions(int arr[], int n) {
        return mergeSort(arr, 0, n - 1);
    }
    
```