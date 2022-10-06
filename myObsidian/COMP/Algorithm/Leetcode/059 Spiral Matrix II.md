---
aliases: [leetcode 059, ]
tags:
  - array
---
Given a positive integer `n`, generate an `n x n` `matrix` filled with elements from `1` to `n2` in spiral order.
```java

public int[][] generateMatrix(int n) {
        // change from retrive to generate
        int[][] res = new int [n][n];
        int i =0,j=0,layer =0,count =0;
        while(count < n*n){
            res[i][j] = count+1;
            if(i==layer && j<n-1-layer) j++;
            else if(j == n-1 -layer&& i<n-1-layer) i++;
            else if(i == n-1-layer &&  j>layer) j--;
            else if(j == layer &&  i>layer){
                i--;
                if(j == layer && i == layer+1&&n!=1) layer++;
            } 
            
            count++;
        }
        return res;
        
    }
-   20/20 cases passed (0 ms)
-   Your runtime beats 100 % of java submissions
-   Your memory usage beats 52.25 % of java submissions (42 MB)
```

