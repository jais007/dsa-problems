### DFS Method

```cpp
 bool dfs(int src, unordered_map<int,vector<int>> &adj,vector<int> &visited, vector<int> &recS){
        visited[src] = 1;
        recS[src] = 1;
        for(int node : adj[src]){
            if(!visited[node]){
                if(dfs(node, adj, visited, recS))
                    return true;
            }else if(recS[node]){
                return true;
            }
        }
        recS[src] = 0;
        return false;
    }
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        unordered_map<int,vector<int>> adj;
        vector<int> visited(2001, 0);
        vector<int> recS(2001, 0);
        for(auto it : prerequisites){
            adj[it[1]].push_back(it[0]);
        }
        for(int i=0;i<numCourses;i++){
            if(!visited[i]){
                if(dfs(i,adj,visited,recS)) return false;
            }
        }
        return true;
    }
```

#BFS Method

```cpp
bool iscycle(vector<int> adj[],vector<int> &vis,int id){
        if(vis[id]==1)
            return true;
        if(vis[id]==0){
            vis[id]=1;
            for(auto edge : adj[id]){
                if(iscycle(adj,vis,edge))
                    return true;
            }
        }
        vis[id] = 2;
        return false;
    }
    bool canFinish(int n, vector<vector<int>>& pre) {
        vector<int> adj[n];
        for(auto edge : pre)
            adj[edge[1]].push_back(edge[0]);
        vector<int> vis(n,0);
        
        for(int i=0;i<n;i++){
            if(iscycle(adj,vis,i))
                return false;
        }
        return true;
    }

```