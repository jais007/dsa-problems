
Dijkstra's algorithm
Time complexity: O(Nlog(N) + E), Space complexity: O(N + E)

```java
class Solution {
    public int networkDelayTime(int[][] times, int n, int k) {
        Map<Integer, List<int[]>> graph = new HashMap<>();
        for(int[] time: times){
            graph.putIfAbsent(time[0], new ArrayList<>());
            graph.get(time[0]).add(new int[]{time[1], time[2]});
        }
        
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[0]-b[0]);
        pq.offer(new int[]{0,k});
        boolean[] visited = new boolean[n + 1];
        int[] minDis = new int[n + 1];
        Arrays.fill(minDis, Integer.MAX_VALUE);
        minDis[k] = 0;
        int max = 0;

        while(!pq.isEmpty()){
            int[] curr = pq.poll();
            int currDist = curr[0];
            int currNode = curr[1];
            if(visited[currNode])
                continue;
            visited[currNode] = true;
            max = currDist;
            n--;
            if(graph.containsKey(currNode)){
                for(int[] next : graph.get(currNode)){
                   if(!visited[next[0]] && currDist + next[1] < minDis[next[0]]){
                        pq.offer(new int[]{currDist + next[1], next[0]});
                   }
                }
            }
        }
        return n == 0 ? max : -1;
    }
}
```



Bellman-Ford algorithm
Time complexity: O(N*E), Space complexity: O(N)
```java
public int networkDelayTime_BF(int[][] times, int N, int K) {
    double[] disTo = new double[N];
    Arrays.fill(disTo, Double.POSITIVE_INFINITY);
    disTo[K - 1] = 0;
    for (int i = 1; i < N; i++) {
        for (int[] edge : times) {
            int u = edge[0] - 1, v = edge[1] - 1, w = edge[2];
            disTo[v] = Math.min(disTo[v], disTo[u] + w);
        }
    }
    double res = Double.MIN_VALUE;
    for (double i: disTo) {
        res = Math.max(i, res);
    }
    return res == Double.POSITIVE_INFINITY ? -1 : (int) res;
}
```
