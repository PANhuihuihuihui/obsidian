## Easy
### [001](https://leetcode.cn/problems/two-sum/) Two sum 
- 数据结构使用: [[HasMap]] 
1. 暴力搜索: 注意边界
```java
    public int[] twoSum(int[] nums, int target) {
	    // 考虑特殊情况
		int[] result = {0, 1};
        if (nums.length <= 2) {
            return result;
        }
        for (int i = 0; i < nums.length - 1; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[i] + nums[j] == target) {
                    return new int[] {i, j};
                }
            }
        }

        return new int[] {};
    }
```
2. 二分: 实际上还是暴力搜索 但是双指针同时向中间
```Java
public int[] twoSum(int[] nums, int target) {
	// 考虑特殊情况
	int[] result = {0, 1};
	if (nums.length <= 2) {
		return result;
	}
    for(int i =0;i < nums.length - 1; i++){
	    for (int j = i + 1,k = nums.length - 1; j <=k ; j++,k--){
		    int tmp = target - nums[i];
		    result[0] = i;
		    if(nums[j] ==tmp){
			    result[1] = j; 
			    return result;
			}
			if(nums[k] ==tmp){
			    result[1] = k; 
			    return result;
			}
		    
	    }
    }
    return result;
```
3. 四分： 双二分
```Java
public int[] twoSum(int[] nums, int target) {
	// 考虑特殊情况
	int[] result = {0, 1};
	if (nums.length <= 2) {
		return result;
	}
    for(int i =0,j= nums.length - 1;i <=j; i++,j--){
	    if(nums[i] + nums[j] == target){
		    // lucky
		    result[0] = i;
		    result[1] = j;
		    return result;
		}
		// 不要放在for 里面
		int tmp1 = target - nums[i];
		int tmp2 = target - nums[j];
	    for (int m = i + 1,n = j - 1; m <=n ; m++,n--){
		    //代码好看： 通用的放在外面？ 都可以 
		    if(nums[m] ==tmp1){
			    result[0] = i;
			    result[1] = m; 
			    return result;
			}
			if(nums[m] ==tmp2){
			    result[0] = j; 
			    result[1] = m;
			    return result;
			}
			if(nums[n] ==tmp1){
				result[0] = i;
			    result[1] = n; 
			    return result;
			}
			if(nums[n] ==tmp2){
				result[0] = j; 
			    result[1] = n; 
			    return result;
			}
		    
	    }
    }
    return result;
```

4. HasMap
```Java
import java.util.HashMap;
public int[] twoSum(int[] nums, int target) {
	// 考虑特殊情况
	int[] result = {0, 1};
	if (nums.length <= 2) {
		return result;
	}
	Map<Integer,Integer> hasmap = new HashMap<Integer,Integer>();

	for(int i = 0; i< nums.length; i++){
		int tmp = target-nums[i];
		if(hasmap.containsKey(tmp)){
			result[0] = i; 
			result[1] = hasmap.get(tmp); 
			return result;
		}
		hasmap.put(nums[i],i);

	}

	return result;

}
```
6. HasMap + 二分 best
```Java
public int[] twoSum(int[] nums, int target) {
	// 考虑特殊情况
	int[] result = {0, 1};
	if (nums.length <= 2) {
		return result;
	}
	Map<Integer,Integer> hasmap = new HashMap<Integer,Integer>();
	for(int i =0,j= nums.length - 1;i <=j; i++,j--){
	    if(nums[i] + nums[j] == target){
		    // lucky
		    result[0] = i;
		    result[1] = j;
		    return result;
		}
		int tmp1 = target - nums[i];
		if(hasmap.containsKey(tmp1)){
			result[0] = i; 
			result[1] = hasmap.get(tmp1); 
			return result;
		}
		int tmp2 = target - nums[j];
		if(hasmap.containsKey(tmp2)){
			result[0] = j; 
			result[1] = hasmap.get(tmp2); 
			return result;
		}
		hasmap.put(nums[i],i);
		hasmap.put(nums[j],j);
		
		
}
	
```
## 004 Median of two sorted arrays
