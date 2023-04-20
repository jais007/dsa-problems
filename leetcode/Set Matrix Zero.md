```java
 void setZeroes(vector<vector<int>>& mat) {
        bool firstRow = false;
        bool firstCol = false;

       //step 1
        for(int i=0;i<mat.size();i++){
            for(int j = 0 ; j < mat[i].size() ; j++){
                if(mat[i][j] == 0){
                    if(i == 0) firstRow = true;
                    if(j == 0) firstCol = true;
                    mat[0][j] = 0;
                    mat[i][0] = 0;
                }
            }
        }
        //step 2
         for(int i=1;i<mat.size();i++){
            for(int j = 1 ; j < mat[i].size() ; j++){
                if(mat[0][j] == 0 || mat[i][0] == 0){
                    mat[i][j] = 0;
                }
            }
        }

        if(firstRow){
            for(int i=0;i<mat[0].size();i++){
                 mat[0][i] = 0;
            }
        }
         if(firstCol){
            for(int i=0;i<mat.size();i++){
                 mat[i][0] = 0;
            }
        }
    }
```