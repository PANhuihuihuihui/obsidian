---
aliases: [leetcode 113, ]
tags:
  - dfs
  - tree
---

### Leetcode 113
Given the `root` of a binary tree and an integer `targetSum`, return _all **root-to-leaf** paths where the sum of the node values in the path equals_ `targetSum`_. Each path should be returned as a list of the node **values**, not node references_.

A **root-to-leaf** path is a path starting from the root and ending at any leaf node. A **leaf** is a node with no children.

```java
public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        // one list for tracking 
        // one res for return 
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        trackPathSum(root,targetSum,new ArrayList<Integer>(),res);
        return res;
    }

    public  void trackPathSum(TreeNode node, int targetSum,List<Integer> currPath, List<List<Integer>> res ){
        if(node==null) return;
        currPath.add(node.val);
        if(node.left ==null && node.right == null && node.val ==  targetSum){
            res.add(new ArrayList<Integer>(currPath));// copy? can't work?
        }else{
            trackPathSum(node.left,targetSum-node.val,currPath,res);
            trackPathSum(node.right,targetSum-node.val,currPath,res);
        }
        currPath.remove(currPath.size()-1);// better remove by index
    }
```

Related: [[004 Branch sum|leetcode 112]]
