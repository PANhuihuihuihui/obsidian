---
aliases: [algo 019 , ]
tags:
  - 
---

## Algo 019
#### Problem Statement
Write a function that takes in two non-empty arrays of integers. The function should nd the pair of numbers (one from the rst array, one from the second array) whose absolute difference is closest to zero. The function should return an array containing these two numbers, with the number from the rst array in the rst position. Assume that there will only be one pair of numbers with the smallest difference. 
`Sample input: [-1, 5, 10, 20, 28, 3], [26, 134, 135, 15, 17]`
`Sample output: [28, 26]`

```java
public static int[] smallestDifference(int[] arrayOne, int[] arrayTwo) {
        // sort first
        Arrays.sort(arrayOne);
        Arrays.sort(arrayTwo);
        int one = 0,two =0,currentMin = Integer.MAX_VALUE;
        int[] res = new int[2];
        while(one<arrayOne.length&&two<arrayTwo.length){
            if(Math.abs(arrayOne[one]-arrayTwo[two])<currentMin){
                res[0]= arrayOne[one];
                res[1]= arrayTwo[two];
                currentMin = Math.abs(arrayOne[one]-arrayTwo[two]);
            }
            if (arrayOne[one]>arrayTwo[two]){
                two++;
            }
            else if(arrayOne[one]<arrayTwo[two]){
                one++;
            }
            else{
                return res;
            }
        }
        return res;
    }
```