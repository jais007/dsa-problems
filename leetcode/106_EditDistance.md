```java
int editDistanceUtil(string& S1, string& S2, int i, int j, vector<vector<int>>& dp){
    
    if(i<0)
        return j+1;
    if(j<0)
        return i+1;
        
    if(dp[i][j]!=-1) return dp[i][j];
        
    if(S1[i]==S2[j])
        return dp[i][j] =  0+editDistanceUtil(S1,S2,i-1,j-1,dp);
        
    // Minimum of three choices
    else return dp[i][j] = 1+min(editDistanceUtil(S1,S2,i-1,j-1,dp),
    min(editDistanceUtil(S1,S2,i-1,j,dp),editDistanceUtil(S1,S2,i,j-1,dp)));
    
}

int editDistance(string& S1, string& S2){
    
    int n = S1.size();
    int m = S2.size();
    
    vector<vector<int>> dp(n,vector<int>(m,-1));
    return editDistanceUtil(S1,S2,n-1,m-1,dp);
    
}
```

```java
static int editDistance(String S1, String S2){
    
    int n = S1.length();
    int m = S2.length();
    
    int[][] dp=new int[n+1][m+1];
     for(int i=0;i<=n;i++){
        dp[i][0] = i;
    }
    for(int j=0;j<=m;j++){
        dp[0][j] = j;
    }
    
    for(int i=1;i<n+1;i++){
        for(int j=1;j<m+1;j++){
            if(S1.charAt(i-1)==S2.charAt(j-1))
                dp[i][j] = 0+dp[i-1][j-1];
            
            else dp[i][j] = 1+Math.min(dp[i-1][j-1],Math.min(dp[i-1][j],dp[i][j-1]));
        }
    }
    
    return dp[n][m];
}
```

* Space Optimized
  
```java
static int editDistance(String S1, String S2){
    
    int n = S1.length();
    int m = S2.length();
    
    int[] prev=new int[m+1];
    int[] cur=new int[m+1];
    
    for(int j=0;j<=m;j++){
        prev[j] = j;
    }
    
    for(int i=1;i<n+1;i++){
        cur[0]=i;
        for(int j=1;j<m+1;j++){
            if(S1.charAt(i-1)==S2.charAt(j-1))
                cur[j] = 0+prev[j-1];
            
            else cur[j] = 1+Math.min(prev[j-1],Math.min(prev[j],cur[j-1]));
        }
        prev = (int[])(cur.clone());
    }
    
    return prev[m];
    
}
```
