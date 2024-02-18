```java
class Pair{
    private int x;
    private int y;
    Pair(int x, int y){
        this.x = x;
        this.y = y;
    }

    @Override
    public boolean equals(Object obj)
    { 
        return (((Pair) obj).x == this.x)&&(((Pair) obj).y == this.y);
    }
    
    @Override
    public int hashCode(){
        return Objects.hash(x,y);
    }
}
class Solution {
    public int minAreaRect(int[][] points) {
        Set<Pair> set = new HashSet<>();
        for(int[] point : points){
            set.add(new Pair(point[0], point[1]));
        }

        int ans = Integer.MAX_VALUE;
        for(int i = 0; i < points.length; i++){
            int x1 = points[i][0];
            int y1 = points[i][1];
            for(int j = i + 1; j < points.length; j++){

                int x2 = points[j][0];
                int y2 = points[j][1];
                Pair p1 = new Pair(x1, y2);
                Pair p2 = new Pair(x2, y1);
                if(x1 != x2 && y1 != y2 && set.contains(p1) && set.contains(p2)){
                    ans = Math.min(ans, Math.abs(x2 - x1) * Math.abs(y2 - y1));
                }
            }
            
        }
        return ans == Integer.MAX_VALUE ? 0 : ans;
    }
}
```
