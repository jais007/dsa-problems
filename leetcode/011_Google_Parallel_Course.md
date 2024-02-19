Return the minimum number of semesters needed to take all courses. If there is no way to take all the courses, return -1.

* Analysis: Time & space: O(V + E).

```java

class Solution {
    public int minimumSemesters(int n, int[][] relations) {
        Map<Integer, List<Integer>> adjList = new HashMap<>();
        Queue<Integer> queue = new LinkedList<>();
        int[] indegree = new int[n + 1];
        for(int [] relation : relations){
            int src = relation[0];
            int des = relation[1];
            List<Integer> list = adjList.getOrDefault(src, new ArrayList<>());
            list.add(des);
            adjList.put(src, list);
            indegree[des]++;
        }
        for(int i=1;i<=n;i++){
            if(indegree[i]==0){
                queue.offer(i);
            }
        }

        int sem = 0;
        int numCourses = 0;
        while(!queue.isEmpty()){
            int size = queue.size();
            sem++;
            while(size-- > 0){
                int node = queue.poll();
                numCourses++;
                if(adjList.containsKey(node)){
                    for(Integer neighbour: adjList.get(node)){
                        indegree[neighbour]--;
                        if(indegree[neighbour] == 0){
                            queue.offer(neighbour);
                        }
                    }
                }
            }
        }
        return numCourses == n ? sem : -1; 
    }
}
```