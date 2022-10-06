---
aliases: [leetcode 845 , algo 022]
tags:
  - array
---
## Leetcode 845
You may recall that an array `arr` is a **mountain array** if and only if:
-   `arr.length >= 3`
-   There exists some index `i` (**0-indexed**) with `0 < i < arr.length - 1` such that:
    -   `arr[0] < arr[1] < ... < arr[i - 1] < arr[i]`
    -   `arr[i] > arr[i + 1] > ... > arr[arr.length - 1]`

Given an integer array `arr`, return _the length of the longest subarray, which is a mountain_. Return `0` if there is no mountain subarray.

#### Approach I self
try to literate the array and keep track the direction (up/down)not good because of too many case to condsider.`Failed`
```java
public int longestMountain(int[] arr) {
        if(arr.length < 3) return 0;
        int res = 0, curLongest = 2;
        boolean upwards = false;
        boolean downwards = false;
        for(int i =0;i<arr.length-1;i++){
            if(arr[i]<arr[i+1]){
                if(downwards){
                    curLongest = 2;
                }
                else if(upwards) curLongest++;
                upwards = true;
                downwards = false;
            }
            else if(arr[i]>arr[i+1]){
                curLongest++;
                upwards = false;
                downwards = true;
            }
            else {
                curLongest =2;
                upwards = false;
                downwards = false;
            }
            
            System.out.println(arr[i]+" "+arr[i+1]+": "+curLongest);
        }
     return res;        
    }
```

#### Approach II reconmend
1. find the peak 
2. compare their length
```java
public int longestMountain(int[] arr) {
   if(arr.length < 3) return 0;
   int res = 0;
   for(int i=1;i<arr.length-1;i++){
	  if(arr[i] > arr[i+1] && arr[i]> arr[i-1]){
		 //peak find
		 int left = i-1,right=i+1;
		 // 这里搞错好大一会： 往下看一步， 切记注&& 前后关系
		 while(left>0&& arr[left]>arr[left-1]) left--;
		 while(right<arr.length-1   &&arr[right]>arr[right+1]) right++;
		 if(right-left+1>res) res = right-left+1;
	  }
   }
   return res;
}
```


#### Takeaways
track the status is difficult However, find the matching **pattern** is easy