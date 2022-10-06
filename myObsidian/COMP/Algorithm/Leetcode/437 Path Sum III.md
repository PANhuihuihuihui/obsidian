---
aliases: [leetcode 437 ]
tags:
  - tree
  - bfs
---
Given the `root` of a binary tree and an integer `targetSum`, return _the number of paths where the sum of the values along the path equals_ `targetSum`.
The path does not need to start or end at the root or a leaf, but it must go downwards (i.e., traveling only from parent nodes to child nodes)

### solution
1. self-recursion
```java
class Solution {
    public int pathSum(TreeNode root, int targetSum) {
        // no need to go to the end and just return true
        // but we can't update the targetSum >>> helper need
        // intend to do the recursion
        List<Integer> res = new ArrayList<Integer>();
        pathSumHelper(root,targetSum,0,res);
        return res.size();
    }
    public void pathSumHelper(TreeNode node, int targetSum,int currentSum, List<Integer> res){

        if(node == null) return;
        currentSum = currentSum + node.val; 
        // forget itself == targetSum?
        if(currentSum == targetSum) res.add(1);
        pathSumHelper(node.left,targetSum,currentSum,res);
        pathSumHelper(node.right,targetSum,currentSum,res);
        pathSumHelper(node.left,targetSum,0,res);
        pathSumHelper(node.right,targetSum,0,res);
    }
}

```

2. suggested recursion
```java 
class Solution {
	// Time: O(n+n-1+n-2+...+1) = O((n+1)n/2) = O(N^2) Space O(N)
    int counter = 0;
    public int pathSum(TreeNode root, int targetSum) {
        if (root == null) return 0;
        pathSumHelper(root,targetSum,0L);
        pathSum(root.left,targetSum);
        pathSum(root.right,targetSum);
        return counter;
    }
    public void pathSumHelper(TreeNode node, int targetSum,long currentSum){
        if(node == null) return;
        currentSum = currentSum + node.val; 
        if(currentSum == targetSum) counter++;
        pathSumHelper(node.left,targetSum,currentSum);
        pathSumHelper(node.right,targetSum,currentSum);
        
    }
}
-   Your runtime beats 29.99 % of java submissions
-   Your memory usage beats 81.7 % of java submissions (43.3 MB)
```
3. improved 前缀和 prefix sum
	 there are alot repeat calulate we should try to remember the previous
	 想法  prefix-j - prefix_i = targetSum 我们需要保存之前结点的前缀和。
```java
class Solution {
// Time O(N) space O(N)
    int targetSum, count = 0;
    Map<Long, Integer> map;
    public int pathSum(TreeNode root, int targetSum) {
        if(root == null) return 0;
        this.targetSum = targetSum;
        this.map = new HashMap<>();
        map.put(0, 1); // 表示前缀和为0的节点为空，有一个空。否则若pre_i = targetSum，将错过从root到i这条路径。
        dfs(root, 0);
        return count;
    }
    private void dfs(TreeNode node, int preSum){
        if(node == null) return;
        preSum += node.val;
        count += map.getOrDefault(preSum - targetSum, 0); // #1 累计满足要求的前缀和数量
        map.put(preSum, map.getOrDefault(preSum, 0) + 1); // #2 先累计再put（先#1，再#2）
        dfs(node.left, preSum);
        dfs(node.right, preSum);
        map.put(preSum, map.get(preSum) - 1); // 路径退缩，去掉不再在路径上的当前结点的前缀和。必存在，无需使用getOrDefault。
    }
}
-   Your runtime beats 86.87 % of java submissions
-   Your memory usage beats 34.06 % of java submissions (44.9 MB)
```


Related [[113 Path Sum II]]



