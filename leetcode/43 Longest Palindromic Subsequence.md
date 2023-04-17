* Solution : DP Memoization

```java
    public int solve(String s, int i, int j, int mem[][]){
        if(i > j){
            return 0;
        }
        if(i == j && s.charAt(i) == s.charAt(j)) return 1;
        if(mem[i][j] != -1) return mem[i][j];
        if(s.charAt(i) == s.charAt(j)){
            return mem[i][j] = 2 + solve(s, i + 1, j - 1, mem);
        }
        return mem[i][j] = Math.max(solve(s, i + 1, j, mem), solve(s, i, j - 1, mem));
    }
    public int longestPalindromeSubseq(String s) {
        int n = s.length();
        int [][]mem = new int[n+1][n+1];
        for(int row[] : mem){
            Arrays.fill(row, 0);
        }
        return solve(s, 0, s.length() - 1,mem);
    }


```

* Solution : Tabulation 

```java

  public int longestPalindromeSubseq(String s) {
        int[][] dp = new int[s.length()][s.length()];

        for (int i = s.length() - 1; i >= 0; i--) {
            dp[i][i] = 1;
            for (int j = i + 1; j < s.length(); j++) {
                if (s.charAt(i) == s.charAt(j)) {
                    dp[i][j] = dp[i + 1][j - 1] + 2;
                } else {
                    dp[i][j] = Math.max(dp[i + 1][j], dp[i][j - 1]);
                }
            }
        }

        return dp[0][s.length() - 1];
    }

```