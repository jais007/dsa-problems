```java
class Solution {
    private void letterCombinationsRecursive(String digits, List<String> result, String curr,int idx ,String[] mapping){
        if(idx == digits.length()){
            result.add(curr);
            return;
        }
        String letters = mapping[digits.charAt(idx) - '0'];
        for(int i=0;i<letters.length(); i++){
            letterCombinationsRecursive(digits, result, curr + letters.charAt(i), idx + 1, mapping);
        }
    }
    public List<String> letterCombinations(String digits) {
        List<String> result = new ArrayList<>();
        if(digits == null || digits.length() == 0) return result;

        String[] mapping  =  { "", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz" };

        letterCombinationsRecursive(digits,result,"",0,mapping);
        return result;
    }
}
```