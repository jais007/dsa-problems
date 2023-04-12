```java
class Solution {
    int len = 0;
    public List<List<Integer>> fourSum(int[] nums, int target) {
        len = nums.length;
        Arrays.sort(nums);
        return kSum(nums, target, 0, 4);
    }
	
    public List<List<Integer>> kSum(int[] nums, int target, int start, int k) {
        List<List<Integer>> res = new ArrayList<>();

        // If we have run out of numbers to add, return res.
        if(len - start < k){
            return res;
        }
        
        if (k == 2) {
            return twoSum(nums, target, start);
        }

        // There are k remaining values to add to the sum. The 
        // average of these values is at least target / k.
        long average_value = target / k;
        
        // We cannot obtain a sum of target if the smallest value
        // in nums is greater than target / k or if the largest 
        // value in nums is smaller than target / k.

        if  (nums[start] > average_value || average_value > nums[len - 1]) {
            return res;
        }
    
        for (int i = start; i < len; ++i) {
            if (i == start || nums[i - 1] != nums[i]) {
                List<List<Integer>> subRes  = kSum(nums, target - nums[i], i + 1, k - 1);
                for(List<Integer> list : subRes){
                    list.add(nums[i]);
                    res.add(list);
                }
            }
        }
        return res;
    }
	
    private List<List<Integer>> twoSum(int[] nums, int target, int startIndex){
        
        List<List<Integer>> res = new ArrayList<>();
        if(len - startIndex < 0){
            return res;
        }
        int i = startIndex;
        int j = len - 1;
        while(i < j) {
            //find a pair
        	if(target - nums[i] == nums[j]) {
            	List<Integer> temp = new ArrayList<>();
                temp.add(nums[i]);
                temp.add(nums[j]);
                res.add(temp);
                //skip duplication
                while(i < j && nums[i] == nums[i+1]) i++;
                while(i < j && nums[j-1] == nums[j]) j--;
                i++;
                j--;
                //move left bound
            } else if (target - nums[i] > nums[j]) {
        	    i++;
            //move right bound
        	} else {
            	j--;
            }
        }
        return res;
   }
}
```