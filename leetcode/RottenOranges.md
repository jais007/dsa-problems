```java
 public int orangesRotting(int[][] grid) {
        int n = grid.length;
        int m = grid[0].length;
        int timer = 0;
        Queue<int[]> q = new LinkedList<>();
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                if(grid[i][j] == 2){
                    q.offer(new int[]{i,j});
                }
            }
        }
        int [][]visited = new int[n][m];
        for(int []row : visited)
            Arrays.fill(row, 0);

        int [][]dir = new int[][]{{0, 1}, { 1, 0}, {0, -1}, {-1, 0}};
        
         while(!q.isEmpty()){
            int size = q.size();
            for(int x=0;x<size;x++){
                int r = q.peek()[0];
                int c = q.peek()[1];
                q.poll();
                visited[r][c] = 1;
                for(int i=0;i<dir.length;i++){
                    int newRow = r + dir[i][0];
                    int newCol = c + dir[i][1];
                    if(newRow >= 0 && newRow < n && newCol >= 0 && newCol < m &&
                             visited[newRow][newCol] == 0 && grid[newRow][newCol] == 1){
                         q.offer(new int[]{newRow, newCol});
                         grid[newRow][newCol] = 2;
                    }
                }
            }
            if(q.isEmpty()) break;
            timer++;
         }
         for(int i=0;i<n;i++){
             for(int j=0;j<m;j++){
                 if(grid[i][j]==1) return -1;
             }
         }
        return timer;
    }
    ```
