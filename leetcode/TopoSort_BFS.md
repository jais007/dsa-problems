```java
class Solution
    {
            public boolean isCyclic(int N, ArrayList<ArrayList<Integer>> adj) {
                int topo[] = new int[N];
                int indegree[] = new int[N];
                
                //finding indegree
                for(int i = 0;i<N;i++) {
                    for(Integer it: adj.get(i)) {
                        indegree[it]++;
                    }
                }
                
                
                Queue<Integer> q = new LinkedList<Integer>();
                for(int i = 0;i<N;i++) {
                    //adding nodes to queue with indegree = 0
                    if(indegree[i] == 0) {
                        q.add(i);
                    }
                }
                
                int cnt = 0;
                int ind=0;
                
                while(!q.isEmpty()) {
                    Integer node = q.poll();
                    topo[ind++] = node;
                    cnt++;
                    //getting neighbour nodes of popped node and decreasing  their 
                    indegree by1
                    for(Integer it: adj.get(node)) {
                        indegree[it]--;
                        if(indegree[it] == 0) {
                            q.add(it);
                        }
                    }
                }
                 //printing topological ordering of nodes
                for (int i=0;i< topo.length;i++){
                    System.out.print(topo[i]+" ");
                }
                if(cnt == N) return false;
                return true;
            }
        }
       ``` 
