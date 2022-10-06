---
aliases: [leetcode 054 ,algo 021 ]
tags:
  - array
---
## Leetcode 054
Given an `m x n` `matrix`, return _all elements of the_ `matrix` _in spiral order_.
```
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]
```

#### Approach I self
```java
public List<Integer> spiralOrder(int[][] matrix) {
        // find out the rule of change i j
        int i =0,j=0,layer =0,count =0;
        int m = matrix.length,n= matrix[0].length;
        List<Integer> res = new ArrayList<Integer>();
        // layer 1 pass;
        while(count <= m*n-1){
            res.add(matrix[i][j]);
            if(i==layer && j<n-1-layer) j++;
            else if(j == n-1 -layer&& i<m-1-layer) i++;
            else if(i == m-1-layer &&  j>layer) j--;
            else if(j == layer &&  i>layer){
                i--;
                if(j == layer && i == layer+1&&n!=1) layer++;
            } 
            
            count++;
        }
        return res;

    }
-   23/23 cases passed (0 ms)
-   Your runtime beats 100 % of java submissions
-   Your memory usage beats 90.89 % of java submissions (40.4 MB)
```
find the traverse rule;

## Approach II
```java
public static List<Integer> spiralTraverse(int[][] array) {
        if (array.length == 0) return new ArrayList<Integer>();
        var result = new ArrayList<Integer>(); var startRow = 0;
        var endRow = array.length - 1;
        var startCol = 0;
        var endCol = array[0].length - 1;
        while (startRow <= endRow && startCol <= endCol) {
            for (int col = startCol; col <= endCol; col++) {
                result.add(array[startRow][col]); 
            }
            for (int row = startRow + 1; row <= endRow; row++) { 
                result.add(array[row][endCol]);
            }
            for (int col = endCol - 1; col >= startCol; col--) { 
                if (startRow == endRow) break; 
                result.add(array[endRow][col]);
            }
            for (int row = endRow - 1; row > startRow; row--) { 
                if (startCol == endCol) break; 
                result.add(array[row][startCol]);
            }
            startRow++; endRow--; 
            startCol++; endCol--;
        }
        return result; 
    }
```


Related: