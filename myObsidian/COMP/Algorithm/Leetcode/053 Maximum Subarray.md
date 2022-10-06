---
aliases: [leetcode 053]
tags:
  - divide-conquer
  - array
  - dynamic-programming
---
Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return _its sum_.

A **subarray** is a **contiguous** part of an array.
**Follow up:** If you have figured out the `O(n)` solution, try coding another solution using the **divide and conquer** approach, which is more subtle.

#### Approach I DP
dp(i) = dp(i-1)+arr[i],dp(i-1) 
```java
// Time:O(N) Space O(N)
public int maxSubArray(int[] nums) {
   int[] dp = new int[nums.length];
   dp[0] =nums[0];
   int res = dp[0];
   for(int i =1;i<nums.length;i++){
	  dp[i] = nums[i];
	  dp[i] = Math.max(dp[i-1]+nums[i],dp[i]);
	  if(dp[i]>res) res = dp[i];
   }
   return res;
}

-   Your runtime beats 74.36 % of java submissions
-   Your memory usage beats 85.91 % of java submissions (52.5 MB)
```

#### Approach II
improve the space(Noticed that we not using the value of dp before previous)
```java
public int maxSubArray(int[] nums) {
int pre = 0;
        int res = nums[0];
        for (int num : nums) {
            pre = Math.max(pre + num, num);
            res = Math.max(res, pre);
        }
        return res;

}
-   209/209 cases passed (3 ms)
-   Your runtime beats 25.82 % of java submissions
-   Your memory usage beats 10.78 % of java submissions (82 MB)
public int maxSubArray(int[] nums) {
   int pre = 0;
   int res = nums[0];
   for (int num : nums){
	  pre = (pre + num> num) ? pre+num : num;
	  if(pre>res) res = pre;
   }
   return res;
}
-   209/209 cases passed (2 ms)
-   Your runtime beats 74.36 % of java submissions
-   Your memory usage beats 62.07 % of java submissions (73.5 MB)
```