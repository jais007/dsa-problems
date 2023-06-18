```java
   static int[] topoSort(int V, ArrayList<ArrayList<Integer>> adj) 
    {
        // add your code here
        Stack<Integer> stack=new Stack<>();
        boolean[] visited=new boolean[V];
        
        for(int i=0;i<V;i++){
            if(!visited[i]){
                dfs(visited,stack,adj,i);
            }
        }
        int[] arr=new int[V];
        int i=0;
        while(!stack.isEmpty()){
            arr[i]=stack.pop();
            i++;
        }
        return arr;
    }
    static void dfs(boolean[] visited,Stack<Integer> stack, ArrayList<ArrayList<Integer>> adj,int node){
        visited[node]=true;
        for(int i : adj.get(node)){
            if(!visited[i]){
                dfs(visited,stack,adj,i);
                
            }
        }
        stack.push(node);
    }
```
