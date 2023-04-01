### FloodFill
```
class Solution {
    private void dfs(int[][] image, int sr, int sc, int originalColor, int newColor){
        if(sr < 0 || sr >= image.length || sc < 0 || sc >= image[0].length || 
                 image[sr][sc] == newColor || image[sr][sc] != originalColor) 
            return;
        image[sr][sc] = newColor;
        dfs(image, sr + 1, sc, originalColor, newColor);
        dfs(image, sr, sc + 1, originalColor, newColor);
        dfs(image, sr - 1, sc, originalColor, newColor);
        dfs(image, sr, sc - 1, originalColor, newColor);
    }
    public int[][] floodFill(int[][] image, int sr, int sc, int color) {
       dfs(image,sr,sc,image[sr][sc], color);
       return image;
    }
}
```