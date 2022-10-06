---
aliases: [leetcode 322, ]
tags:
  - dp
---
### Leetcode 322
You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.
Return _the fewest number of coins that you need to make up that amount_. If that amount of money cannot be made up by any combination of the coins, return `-1`.
You may assume that you have an infinite number of each kind of coin.
### Aprroach self
```java
    public int coinChange(int[] coins, int amount) {
        //hasmap dp[chage] = coinN
        if (amount < 1) return 0;
        Map<Integer,Integer> dp = new HashMap<Integer,Integer>();
        dp[0] =0;
        for(int i =1; i<=amount;i++){
            for(int j = 0;j<coins.length;j++){
                if(i-coins[j]>0&&dp[i-coins[j]]+1<dp[i]){
                    dp[i] = dp[i-coins[j]]+1;
                }
                
            }
        }
        return dp[amount];
        
    }
```
1. HashMap: put(key,value)
2. can not deal with the -1 situation;
Consider that the max return should be less than amount.
3. Array.fill()
4. Hashmap not need, cause we use 

### Approach self-improve
```java
public int coinChange(int[] coins, int amount) {
   //hasmap dp[chage] = coinN
   if (amount < 1) return 0;
   int[] dp=new int[amount+1];
   Arrays.fill(dp,amount+1);
   dp[0]=0;
   for(int i =1; i<=amount;i++){
	  for(int coin:coins){
		 if(coin<=i){
			dp[i] = Math.min(dp[i-coin]+1,dp[i]);
		 }
	  }
   }
   return dp[amount]>amount? -1 : dp[amount];
   
}
```
-   189/189 cases passed (16 ms)
-   Your runtime beats 94.12 % of java submissions
-   Your memory usage beats 91.53 % of java submissions (42.1 MB)

### Approach BFS
BFS to find the shortest path: (because unweighted)
```java
public int coinChange(int[] coins, int amount) {
	Queue<Integer> q = new LinkedList<>();
	boolean[] vstd = new boolean[amount+1];
	int cs =0;
	q.add(0);
	while(!q.isEmpty()){
		int n = q.size();
		for(int i=0;i<n;i++) {
			 int sum = q.poll();
			 if(sum==amount) {
				return cs;
			 }
			 if(sum>amount || vstd[sum]) {
				continue;
			 }
			 vstd[sum]=true;
			 for(int coin:coins) {
				q.add(sum+coin);
			 }
		}
		cs++;
	}
	

}
```
-   189/189 cases passed (225 ms)
-   Your runtime beats 8 % of java submissions
-   Your memory usage beats 5.58 % of java submissions (117.3 MB)
- slow because use some complex data structure

 1. BFS: queue (define) DFS: Stack(recursion/define)
 2. 


#### Related 
