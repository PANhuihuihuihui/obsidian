---
aliases: [leetcode 112 ]
tags:
  - tree
  - bfs
---
Related:  [[004 Branch sum]], [[113 Path Sum II]] [[437 Path Sum III]]

### Leetcode 112 Path Sum

Given the `root` of a binary tree and an integer `targetSum`, return `true` if the tree has a **root-to-leaf** path such that adding up all the values along the path equals `targetSum`.

A **leaf** is a node with no children.
### Solution I
1. self recursion similar to pervious
```java
    public boolean hasPathSum(TreeNode root, int targetSum) {
        return calculatePathSum(root,targetSum,0);
        
    }
    public boolean calculatePathSum(TreeNode node, int targetSum,int runningSum){
        if (node == null) return false;
        runningSum = runningSum + node.val;

        if (node.left ==null && node.right ==null){
            if (runningSum == targetSum){
                return true;
            }
            return false;
        }
        boolean left = calculatePathSum(node.left,targetSum,runningSum);
        boolean right = calculatePathSum(node.right,targetSum,runningSum);
        return ( left || right);
    }
-   117/117 cases passed (1 ms)
-   Your runtime beats 63.31 % of java submissions
-   Your memory usage beats 74.96 % of java submissions (43.3 MB)
```
2.  suggest recursion methond
提升了memory usage
```java
public boolean hasPathSum(TreeNode root, int targetSum) {
    // recursion method
    if (root == null) return false;
    if (root.left == null && root.right == null && root.val == sum) return true;
    return hasPathSum(root.left, sum - root.val) || hasPathSum(root.right, sum - root.val);
}
-   Your runtime beats 63.31 % of java submissions
-   Your memory usage beats 82.76 % of java submissions (43.1 MB) 
```
注意space O(H)  where H is height of tree
- worest: O(N) = O(H)
- avearge binary tree: O(H) = O(logN)

#### Solution II dfs FILO
用stack 记录信息 
```java
public boolean hasPathSum(TreeNode root, int targetSum) {
        // recursion method
        if (root == null) {return false;}
        Stack<TreeNode> path = new Stack<>();
        Stack<Integer> sub = new Stack<>();
        path.push(root);
        sub.push(root.val);
        while (!path.isEmpty()) {
            TreeNode temp = path.pop();
            int tempVal = sub.pop();
            if (temp.left == null && temp.right == null) {if (tempVal == targetSum) return true;}
            else {
                if (temp.left != null) {
                    path.push(temp.left);
                    sub.push(temp.left.val + tempVal);
                }
                if (temp.right != null) {
                    path.push(temp.right);
                    sub.push(temp.right.val + tempVal);
                }
            }
        }
        return false;
        
    }

-   Your runtime beats 8.26 % of java submissions
-   Your memory usage beats 18.62 % of java submissions (44.2 MB)
```

#### Solution III
bfs queue FIFO
```java
public boolean hasPathSum(TreeNode root, int sum) {
        if (root == null) {
            return false;
        }
        Queue<TreeNode> queNode = new LinkedList<TreeNode>();
        Queue<Integer> queVal = new LinkedList<Integer>();
        queNode.offer(root);
        queVal.offer(root.val);
        while (!queNode.isEmpty()) {
            TreeNode now = queNode.poll();
            int temp = queVal.poll();
            if (now.left == null && now.right == null) {
                if (temp == sum) {
                    return true;
                }
                continue;
            }
            if (now.left != null) {
                queNode.offer(now.left);
                queVal.offer(now.left.val + temp);
            }
            if (now.right != null) {
                queNode.offer(now.right);
                queVal.offer(now.right.val + temp);
            }
        }
        return false;
    }

```