
There are n cities. Some of them are connected, while some are not. If city a is connected directly with city b, and city b is connected directly with city c, then city a is connected indirectly with city c.

A province is a group of directly or indirectly connected cities and no other cities outside of the group.

You are given an n x n matrix isConnected where isConnected[i][j] = 1 if the ith city and the jth city are directly connected, and isConnected[i][j] = 0 otherwise.

Time complexity: O(n*n).

```java
class Solution {
 

    public int findCircleNum(int[][] isConnected) {
         int n = isConnected.length;
        int[] parent = new int[n];

        for (int i = 0; i < n; i++) {
            parent[i] = i; 
        }

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (i != j && isConnected[i][j] == 1) {
                    // Merge the provinces of cities i and j
                    union(parent, i, j);
                }
            }
        }

        // Count the number of unique parent nodes, which represents the number of provinces
        HashMap<Integer, Boolean> provinces = new HashMap<>();
        for (int i = 0; i < n; i++) {
            provinces.put(find(parent, i), true);
        }

        return provinces.size();
    }

    private int find(int[] parent, int city) {
       
        if (parent[city] != city) {
            parent[city] = find(parent, parent[city]); 
        }
        return parent[city];
    }

    private void union(int[] parent, int city1, int city2) {
        // Merge the provinces of city1 and city2
        int root1 = find(parent, city1);
        int root2 = find(parent, city2);

        if (root1 != root2) {
            parent[root1] = root2;
        }
    }
}
```
