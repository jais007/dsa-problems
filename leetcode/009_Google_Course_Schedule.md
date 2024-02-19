

```java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        Map<Integer, List<Integer>> graph = new HashMap<>();
        for(int i = 0; i < numCourses; i++) graph.put(i, new ArrayList<>());

        for(int[] pre : prerequisites){
            int first = pre[0];
            int second = pre[1];
            graph.get(first).add(second);
        }

        boolean[] visited = new boolean[numCourses];
        for(int i = 0; i < numCourses; i++){
            if(!visited[i]){
                boolean hasCycle = hasCycle(graph, i, visited, new boolean[numCourses]);
                if(hasCycle) return false;
            }
        }
        return true;
    }

    private boolean hasCycle(Map<Integer, List<Integer>> graph, int start, boolean[] visited, boolean[] dfsVisited){
        visited[start] = true;
        dfsVisited[start] = true;
        boolean ans = false;
        for(int neighbour : graph.get(start)){
            if(!visited[neighbour]){
                ans = hasCycle(graph, neighbour, visited, dfsVisited);
                if(ans) return ans;
            }else if(dfsVisited[neighbour]){
                return true;
            }
        }
        dfsVisited[start] = false;
        return ans;
    }
}

```