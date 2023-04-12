*  https://www.geeksforgeeks.org/count-of-pairs-of-strings-whose-concatenation-forms-a-palindromic-string/

```java
int getCount(int N, vector<string>& s){
	// Stores frequency array
	// and its count
	map<vector<int>, int> mp;

	// Total number of pairs
	int ans = 0;

	for (int i = 0; i < N; i++) {

		// Initializing array of size 26
		// to store count of character
		vector<int> a(26, 0);

		// Counting occurrence of each
		// character of current string
		for (int j = 0; j < s[i].size(); j++) {

			a[s[i][j] - 'a']++;
		}

		// Convert each count to parity(0 or 1)
		// on the basis of its frequency
		for (int j = 0; j < 26; j++) {

			a[j] = a[j] % 2;
		}

		// Adding to answer
		ans += mp[a];

		// Frequency of single character
		// can be possibly changed,
		// so change its parity
		for (int j = 0; j < 26; j++) {

			vector<int> changedCount = a;

			if (a[j] == 0)
				changedCount[j] = 1;
			else
				changedCount[j] = 0;

			ans += mp[changedCount];
		}

		mp[a]++;
	}

	return ans;
}
```