
BFS : Indegree

```java
class Solution {
  Stack<Integer> stack;
  public int[] findOrder(int numCourses, int[][] prerequisites) {
    stack = new Stack<>();
    Map<Integer, List<Integer>> adjList = new HashMap<Integer, List<Integer>>();
 
    for (int i = 0; i < prerequisites.length; i++) {
      int dest = prerequisites[i][0];
      int src = prerequisites[i][1];
      List<Integer> list = adjList.getOrDefault(src, new ArrayList<Integer>());
      list.add(dest);
      adjList.put(src, list);
    }
    boolean[] visited = new boolean[numCourses];
    boolean[] path = new boolean[numCourses];
    for(int i=0;i<numCourses;i++){
        if(!dfs(i, visited, path, adjList)){
                 return new int[0];
        }
    }
    int i = 0;
    int[] res = new int[numCourses];
    while(!stack.isEmpty()){
        res[i++] = stack.pop();
    }
    return res;
  }
  private boolean dfs(int root, boolean[] visited, boolean[] path, Map<Integer, List<Integer>> adjList){
      //node has already been visited and added to res
      if(visited[root]){
          return true;
      }
     // we are encoutering a node already on the path, aka there is a cycle
     if(path[root]) {
            return false;
     }
    path[root] = true; 
      if(adjList.containsKey(root)){
        for(Integer node : adjList.get(root)){
           if(!dfs(node, visited,path, adjList)){
               return false;
           }
        }
    }
    stack.push(root);
    visited[root] = true; 
    return true;
  }
}

```