
Method Trie
Time: O(m * m * n + L), space: O(m * n + L * m)

```java
    class Trie {
        Trie[] sub = new Trie[26];
        LinkedList<String> suggestion = new LinkedList<>();
    }
    public List<List<String>> suggestedProducts(String[] products, String searchWord) {
        Trie root = new Trie();
        for (String p : products) { // build Trie.
            insert(p, root); // insert a product into Trie.
        }
        return search(searchWord, root);
    }
    private void insert(String p, Trie root) {
        Trie t = root;
        for (char c : p.toCharArray()) { // insert current product into Trie.
            if (t.sub[c - 'a'] == null)
                t.sub[c - 'a'] = new Trie();
            t = t.sub[c - 'a'];
            t.suggestion.offer(p); // put products with same prefix into suggestion list.
            Collections.sort(t.suggestion);
            if (t.suggestion.size() > 3) // maintain 3 lexicographically minimum strings.
                t.suggestion.pollLast();        
        }
    }
    private List<List<String>> search(String searchWord, Trie root) {
        List<List<String>> ans = new ArrayList<>();
        for (char c : searchWord.toCharArray()) { // search product.
            if (root != null) // if there exist products with current prefix.
                root = root.sub[c - 'a'];
            ans.add(root == null ? Arrays.asList() : root.suggestion); // add it if there exist products with current prefix.
        }
        return ans;
    }
```

Method : BS
Time: O((n + L) * m * logn), space: O(L * m)

```java
    public List<List<String>> suggestedProducts(String[] products, String searchWord) {
        List<List<String>> ans = new ArrayList<>();
        Arrays.sort(products); // sort products.
        for (int i = 1; i <= searchWord.length(); ++i) {
            String cur = searchWord.substring(0, i);
            int k = Arrays.binarySearch(products, cur);
            while (k > 0 && cur.equals(products[k - 1])) // in case there are more than 1 cur in products.
                --k; // find the first one. 
            if (k < 0) // no cur in products. 
                k = ~k; // find the first one larger than cur.
            List<String> suggestion = new ArrayList<>();
            for (int j = k + 3; k < products.length && k < j && products[k].startsWith(cur); ++k)
                suggestion.add(products[k]);
            ans.add(suggestion);
        }
        return ans;
    }
```

```java

