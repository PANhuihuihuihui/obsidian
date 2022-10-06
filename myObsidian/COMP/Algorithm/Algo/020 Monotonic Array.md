---
aliases: [leetcode 896 , algo 020 ]
---

## Leetcode 896
An array is monotonic if it is either monotone increasing or monotone decreasing.
An array nums is monotone increasing if for all i <= j, nums[i] <= nums[j]. An array nums is monotone decreasing if for all i <= j, nums[i] >= nums[j].
Given an integer array nums, return true if the given array is monotonic, or false otherwise.

#### Approach I self
```java
public boolean isMonotonic(int[] nums) {
        // speciall case
        if(nums.length <=2) return true;
        // find direction
        int before =0, next =1;
        while(nums[before] == nums[next]){
            before++;
            next++;
            if(next == nums.length-1) return true;
        }
        
        boolean upwards;
        if(nums[before] > nums[next]){
            upwards = true;
        }
        else{
            upwards = false;
        }
        while(next <= nums.length-1){
            if(upwards&& nums[before] < nums[next]){
                return false;
                
            }
            if(!upwards&& nums[before] > nums[next]){
                return false;
            }
            before++;
            next++;
        }
        return true;
    }
-   371/371 cases passed (2 ms)
-   Your runtime beats 93.15 % of java submissions
-   Your memory usage beats 59.99 % of java submissions (92.9 MB)
```
not concise enough,  we can slove by a simple for loop with two direction judgement.

#### Approach II Recomend
```java
public boolean isMonotonic(int[] nums) {
	var isNonDecreasing = true;  
	var isNonIncreasing = true;  
	for (int i = 1; i < array.length; i++) {
		if (array[i] < array[i - 1]) isNonDecreasing = false;  
		if (array[i] > array[i - 1]) isNonIncreasing = false; 
	}
	return isNonDecreasing || isNonIncreasing; 
}
-   Your runtime beats 52.58 % of java submissions
-   Your memory usage beats 75.41 % of java submissions (92.6 MB)
```