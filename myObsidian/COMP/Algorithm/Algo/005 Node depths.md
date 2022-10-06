---
aliases: [leetcode , algo 005]
tags:
  - tree
---
Given a Binary Tree, we are asked to find the depth of each node in the tree and return the sum of all nodes' depths. The depth of the root node is `0`.

Example:
```
Binary tree:
             1
           /   \
          2     3
        /   \
       4     5

Output: 6
Explanation:
                    1 --- depth: 0
                  /   \
    depth: 1 --- 2     3 --- depth: 1
               /   \
 depth: 2 --- 4     5 --- depth: 2

sum = 0 + 1 + 1 + 2 + 2 = 6
```

#### Solution I Recursion
```java
import java.util.*;
class Program {
// Time O(N) Space O(N) banlance O(logN) where logN is height of the tree
	int sumOfDepth = 0;
	public static int nodeDepths(BinaryTree root) {
		sumDepthsHelper(root,0);
		return sumOfDepth;
		
	}
	public void sumDepthsHelper(BinaryTree root,int currDepth){
		if(node == null) return ;
		sumOfDepth+=currDepth;
		sumDepthsHelper(node.left,currDepth+1);
		sumDepthsHelper(node.right,currDepth+1);
	}
}

```
suggest improved
```java
public static int nodeDepths(BinaryTree root) {
    return nodeDepthsHelper(root, 0);
  }
  public static int nodeDepthsHelper(BinaryTree root, int depth) {
    if (root == null) return 0;
    return depth + nodeDepthsHelper(root.left, depth + 1) + nodeDepthsHelper(root.right, depth + 1);
}
```

#### Solution II Stack
```java
class Program {
  // Average case: when the tree is balanced
  // O(n) time | O(h) space - where n is the number of nodes in
  // the Binary Tree and h is the height of the Binary Tree  
  public static int nodeDepths(BinaryTree root) {
	int sumOfDepths = 0;
	List<Level> stack = new ArrayList<Level>();
	stack.add(new Level(root, 0));
	while (stack.size() > 0) {
	      Level top = stack.remove(stack.size() -1);
	      BinaryTree node = top.root;
	      int depth = top.depth;
	      if (node == null) continue;
	      sumOfDepths += depth;
	      stack.add(new Level(node.left, depth + 1));
	      stack.add(new Level(node.right, depth + 1));
	}
	
	    return sumOfDepths;
	  }
```






