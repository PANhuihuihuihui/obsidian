---
aliases: [leetcode 271]
tags:
  - hashtable
  - array
---
Given an integer array `nums`, return `true` if any value appears **at least twice** in the array, and return `false` if every element is distinct.

#### Approach I
```java
public boolean containsDuplicate(int[] nums) {
   Set<Integer> set = new HashSet<Integer>();
   for(int i:nums){
	  if(!set.add(i)) return true;
   }
   return false;
}
```

#### Approach II
```java
public boolean containsDuplicate(int[] nums) {
   Arrays.sort(nums);
   int n = nums.length;
   for (int i = 0; i < n - 1; i++) {
	  if (nums[i] == nums[i + 1]) {
		 return true;
	  }
   }
   return false;
}
```

#### Takeaways
1. HashSet.add() 有返回值 表示成不成功
2. sort 也是一种方法