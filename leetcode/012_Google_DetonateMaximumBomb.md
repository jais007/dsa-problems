
```java

class Solution {
    public int maximumDetonation(int[][] bombs) {
        Map<Integer, List<Integer>> graph = new HashMap<>();
        int n = bombs.length;

        for(int i = 0; i < n; i++){
            for(int j = 0; j < n; j++){
                if(i == j) continue;
                
                int x1 = bombs[i][0];
                int y1 = bombs[i][1];
                int r1 = bombs[i][2];

                int x2 = bombs[j][0];
                int y2 = bombs[j][1];
                int r2 = bombs[j][2];
            
                long xDistance = (long) Math.pow((x2 - x1), 2);
                long yDistance = (long) Math.pow((y2 - y1), 2);
                long distance = xDistance + yDistance;
                
                
                if(distance <= (long)r1 * r1){
                    if(graph.get(i) == null){
                        graph.put(i, new ArrayList<>());
                    }
                    graph.get(i).add(j);
                }
            }
        }

        System.out.println(graph);
        int ans = 0;
        for(int i = 0; i < n; i++){
            int dist = dfs(graph, i, n, new HashSet<>());
            ans = Math.max(ans, dist);
        }
        return ans;
    }

    private int dfs(Map<Integer, List<Integer>> graph, int cur, int n, HashSet<Integer> visited){
        visited.add(cur);
        int count = 1;
        for (int neib : graph.getOrDefault(cur, new ArrayList<>())) {
            if (!visited.contains(neib)) {
                count += dfs(graph, neib, n, visited);
            }
        }
        return count;
    }
}
```