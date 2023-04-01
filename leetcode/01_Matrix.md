### 0 1 Matrix

```java
int dir[4][2] = {{0,1},{0,-1}, {1,0}, {-1,0}};
    vector<vector<int>> updateMatrix(vector<vector<int>>& mat) {
        int m = mat.size();
        int n = mat[0].size();
        queue<pair<int,int>> q;
        vector<vector<int>> ans(m , vector<int>(n, -1));
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(mat[i][j] == 0){
                    q.push({i,j});
                    ans[i][j] = 0;
                }
            }
        }
        while(!q.empty()){
          int r = q.front().first;
          int c = q.front().second;
          q.pop();
          for(int x = 0 ; x < 4 ; x ++){
            int newR = r + dir[x][0];
            int newC = c + dir[x][1];
            if(newR >= 0 && newC >=0 && newR < mat.size() && newC < mat[0].size() && ans[newR][newC] == -1){
              q.push({newR, newC});
              ans[newR][newC] = ans[r][c] + 1;
            }
          } 
        }
       return ans;
    }
```