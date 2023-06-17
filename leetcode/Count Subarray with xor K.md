
```java
public static int subarraysXor(ArrayList<Integer> arr, int x) {
		// Write your code here.
		int xor = 0;
		int cnt = 0;
		// xor = y ^ x;
		// y = xor ^ x;
		Map<Integer, Integer> map = new HashMap<>();
		for(int i = 0;i < arr.size(); i++){
			xor = xor ^ arr.get(i);

			if(xor == x) cnt++;

			int y = xor ^ x;
			if(map.containsKey(y)){
				cnt+=map.get(y);
			}
			int c = map.getOrDefault(xor, 0);
			map.put(xor, c + 1);
		}
	return cnt; 	
	}
```
