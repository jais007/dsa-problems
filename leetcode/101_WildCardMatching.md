* Approch 1
  
  ```java
  bool isMatch(string s, string p) {
        vector<vector<bool>> dp(s.length()+1,vector<bool>(p.length()+1));
        dp[0][0]=true;
        for(int i=1;i<=s.length();i++) dp[i][0]=false;
        for(int i=1;i<=p.length();i++) {
             if(p[i-1]=='*'){
                 dp[0][i]=dp[0][i-1];
             }else{
                 dp[0][i]=false;
             }
        }
        for(int i=1;i<=s.length();i++){
            for(int j=1;j<=p.length();j++){
                  if(s[i-1]==p[j-1] || p[j-1]=='?'){
                      dp[i][j]=dp[i-1][j-1];
                  }
                  else if(p[j-1]=='*'){
                      dp[i][j]=dp[i][j-1]||dp[i-1][j];
                  }else{
                      dp[i][j]=false;
                  }
            }
        }
        return dp[s.length()][p.length()];
    }
    ```
* Approch 2
  ```java
   bool isMatch(string str, string pattern) {
        int s = 0, p = 0, match = 0, starIdx = -1;            
        while (s < str.length()){ 
            if (p < pattern.length()  && (pattern[p] == '?' || str[s] == pattern[p])){
                s++;
                p++;
            }
            else if (p < pattern.length() && pattern[p] == '*'){
                starIdx = p;
                match = s;
                p++;
            }
            else if (starIdx != -1){
                p = starIdx + 1;
                match++;
                s = match;
            }
            else 
                return false;
        }
        
        while (p < pattern.length() && pattern[p] == '*')
            p++;
        return p == pattern.length();
}
```
