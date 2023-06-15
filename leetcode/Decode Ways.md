
```java

public int numDecodings(String s) {
    if (s == null || s.length() == 0) {
        return 0;
    }
    char[] chars = s.toCharArray();
    int[] dp = new int[chars.length];
    dp[0] = chars[0] == '0' ? 0 : 1;
    for (int i = 1; i < chars.length; i++) {
        char current = chars[i];
        char prev = chars[i - 1];
        if (current >= '1' && current <= '9') {
            dp[i] = dp[i - 1];
        }
        if ((prev == '1' && current >= '0' && current <= '9') ||
                (prev == '2' && current >= '0' && current <= '6')) {
            dp[i] += i >= 2 ? dp[i - 2] : 1;
        }
    }
    return dp[chars.length - 1];
}

```