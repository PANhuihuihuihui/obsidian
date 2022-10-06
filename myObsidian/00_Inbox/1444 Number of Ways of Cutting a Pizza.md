---
aliases: [leetcode 1444 , ]
tags:
  - prefix-sum
  - dp
  - dfs
---
### Leetcode 1444
Given a rectangular pizza represented as a `rows x cols` matrix containing the following characters: `'A'` (an apple) and `'.'` (empty cell) and given the integer `k`. You have to cut the pizza into `k` pieces using `k-1` cuts. 
For each cut you choose the direction: vertical or horizontal, then you choose a cut position at the cell boundary and cut the pizza into two pieces. If you cut the pizza vertically, give the left part of the pizza to a person. If you cut the pizza horizontally, give the upper part of the pizza to a person. Give the last piece of pizza to the last person.
_Return the number of ways of cutting the pizza such that each piece contains **at least** one apple._ Since the answer can be a huge number, return this modulo 10^9 + 7.

```java
 public int ways(String[] pizza, int k) {
        int m = pizza.length, n = pizza[0].length();
        Integer[][][] dp = new Integer[k][m][n];
        int[][] preSum = new int[m+1][n+1]; // preSum[r][c] is the total number of apples in pizza[r:][c:]
        for (int r = m - 1; r >= 0; r--)
            for (int c = n - 1; c >= 0; c--)
                preSum[r][c] = preSum[r][c+1] + preSum[r+1][c] - preSum[r+1][c+1] + (pizza[r].charAt(c) == 'A' ? 1 : 0);
        return dfs(m, n, k-1, 0, 0, dp, preSum);
    }
    int dfs(int m, int n, int k, int r, int c, Integer[][][] dp, int[][] preSum) {
        if (preSum[r][c] == 0) return 0; // if the remain piece has no apple -> invalid
        if (k == 0) return 1; // found valid way after using k-1 cuts
        if (dp[k][r][c] != null) return dp[k][r][c];
        int ans = 0;
        // cut in horizontal
        for (int nr = r + 1; nr < m; nr++) 
            if (preSum[r][c] - preSum[nr][c] > 0) // cut if the upper piece contains at least one apple
                ans = (ans + dfs(m, n, k - 1, nr, c, dp, preSum)) % 1_000_000_007;
        // cut in vertical
        for (int nc = c + 1; nc < n; nc++) 
            if (preSum[r][c] - preSum[r][nc] > 0) // cut if the left piece contains at least one apple
                ans = (ans + dfs(m, n, k - 1, r, nc, dp, preSum)) % 1_000_000_007;
        return dp[k][r][c] = ans;
    }
```


```java
    public int ways(String[] pizza, int k) {
        //dfs: if hit the buttom add one
        // number of cuts: n+m-2
        N = pizza.length;//row cut
        M = pizza[0].length();// column cut
        // instead of deal with stirng we choose deal with int
        // 
        int res =0;
    }
    public boolean containsA(String[] pizzaP){
        for(String row:pizzaP){
            for(int i=0;i<row.length();i++){
                if(row.charAt(i) == "A") return true;
            }
        }
        return false;
    }
```


```java
    final int MOD = (int) 1e9+7;
    int m, n, k;
    int[][] sums;
    Integer[][][] dp;
    
    public int ways(String[] pizza, int k) {
        this.k = k;
        m = pizza.length; 
        n = pizza[0].length();
        sums = new int[m+1][n+1];
        for (int i = m-1; i >= 0; i--)
            for (int j = n-1; j >= 0; j--)
                sums[i][j] = (pizza[i].charAt(j) == 'A' ? 1 : 0) 
                                + sums[i+1][j] + sums[i][j+1] - sums[i+1][j+1];
        dp = new Integer[m][n][k+1];
        return wayRec(0, 0, 1);
    }
    
    private int wayRec(int i, int j, int v) {
        if (dp[i][j][v] != null) return dp[i][j][v];
        if (v == k) return dp[i][j][v] = (sums[i][j] > 0 ? 1 : 0);
        int ret = 0;
        for (int r = i; r < m-1; r++) 
            if (sums[i][j] - sums[r+1][j] > 0) ret = (ret + wayRec(r+1, j, v+1)) % MOD;
        for (int c = j; c < n-1; c++)
            if (sums[i][j] - sums[i][c+1] > 0) ret = (ret + wayRec(i, c+1, v+1)) % MOD;
        return dp[i][j][v] = ret;
    }
```