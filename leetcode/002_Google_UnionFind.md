```java
class Solution {
    public int earliestAcq(int[][] logs, int n) {
        Arrays.sort(logs, (a,b) -> a[0] - b[0]);
        
        UnionFind uf = new UnionFind(n);
        int nodesVisited = n;
        for(int[] log : logs){
            int time = log[0];
            int first = log[1];
            int second = log[2];

            if(uf.union(first, second)) {
                nodesVisited--;
            }

            if(nodesVisited == 1) return time;
        }
        return -1;
        
    }
}

class UnionFind {
    int[] parent;
    int[] rank;

    UnionFind(int n){
        this.parent = new int[n];
        this.rank = new int[n];
        for(int i = 0; i < n; i++){
            parent[i] = i;
        }
    }

    public int find(int node){
        if(parent[node] == node) return node;
        return find(parent[node]);
    }

    public boolean union(int node1, int node2){
        int parent1 = find(node1);
        int parent2 = find(node2);

        if(parent1 == parent2) return false;

        if(rank[parent1] > rank[parent2]){
            parent[parent2] = parent1;
        }else if(rank[parent2] > rank[parent1]){
            parent[parent1] = parent2;
        }else{
            parent[parent1] = parent2;
            rank[parent2] += 1;
        }
        return true;
    }


}
```
