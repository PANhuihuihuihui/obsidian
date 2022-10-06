---
aliases: [algo 010]
tags:
  - 
---

## Algo 010

```java
// Time O(logN) Space O(logN)
    public static int binarySearchHelper(int[] array, int target,int begin,int end){
        if (end > begin) return -1;
        int mid = (begin+ end) / 2;
        if(array[mid] > target) binarySearchHelper(array,target,begin,mid-1);
        else if (array[mid] < target) binarySearchHelper(array,target,mid+1,end);
        else return mid
    }
    public static int binarySearch2(int[] array, int target){
        int begin =0, end = array.size();
        while(end> begin){
            int mid = (begin+end)/2;
            if(array[mid] > target){
                end = mid-1;
                continue;
            }
            else if (array[mid]< target){
                begin = mid+1;
                continue;
            }
            else return mid;
        }
        return -1;
    }
```




