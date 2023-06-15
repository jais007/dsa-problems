### Spiral Matrix
```cpp

 vector<int> spiralOrder(vector<vector<int>>& matrix) {
        if (matrix.size() == 0) return {};
        int m = matrix.size();
        int n = matrix[0].size();
        int topLeftToRight = 0,  topRightToBottom = 0,  bottomLeftToTop = m-1, bottomRightToLeft = n - 1;
        vector<int> ans;
        
        while (ans.size() != m * n) {
            for (int i = topLeftToRight; i <= bottomRightToLeft; i++) {
                ans.push_back(matrix[topRightToBottom][i]);
            }
            if (ans.size() == m * n) break;
            topRightToBottom++;
            
            for (int i = topRightToBottom; i <= bottomLeftToTop; i++) {
                ans.push_back(matrix[i][bottomRightToLeft]);
            }
            if (ans.size() == m * n) break;
            bottomRightToLeft--;
            
            for (int i = bottomRightToLeft; i >= topLeftToRight; i--) {
                ans.push_back(matrix[bottomLeftToTop][i]);
            }
            if (ans.size() == m * n) break;
            bottomLeftToTop--;
            
            for (int i = bottomLeftToTop; i >= topRightToBottom; i--) {
                ans.push_back(matrix[i][topLeftToRight]);
            }
            topLeftToRight++;
        }
        return ans;
    }
```