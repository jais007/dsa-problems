```java
  private boolean solve(int start, String s, HashSet<String> dict, Boolean []dp){
        if(start == s.length()){
            return true;
        }
        if(dp[start] != null){
            return dp[start];
        }
        for(int j = start ; j <s.length(); j++){
            String word = s.substring(start, j + 1);
        
            if(dict.contains(word) && solve(j + 1, s, dict, dp)){
                return dp[start] = true;
            }
        }
        return dp[start] = false;
    }
    public boolean wordBreak(String s, List<String> wordDict) {
        HashSet<String> dict = new HashSet<>(wordDict);
        Boolean dp[] = new Boolean[s.length() + 1];
        return solve(0, s, dict, dp);
    }
```    
