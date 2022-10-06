---
aliases: [leetcode 112,algo 004]
tags:
  - tree
  - dfs
  - bfs
---
### Algoexpert 004 
Write a function that takes in a Binary Tree and returns a list of its branch sums ordered from leftmost branch sum to rightmost branch sum. A branch sum is the sum of all values in a Binary Tree branch. A Binary Tree branch is a path of nodes in a tree that starts at the root node and ends at any leaf node.

#### Solution 1
 recursion 
这个recursion 有点像 dfs
```java
import java.util.*;
class Program {
	public static class BinaryTree {
		int value; BinaryTree left; BinaryTree right;
		BinaryTree(int value) { this.value = value; this.left = null; this.right = null;} 
	}
	// O(n) time | O(n) space - where n is the number of nodes in the Bi
	public static List<Integer> branchSums(BinaryTree root) { 
		List<Integer> sums = new ArrayList<Integer>();
		calculateBranchSum(root,0,sums);
		return sums;
	}
	
	public static void calculateBranchSum(BinaryTree node,int runningSum,List<Integer> sums){
		if( node == null) return;
		int newRunningSum = node.value + runningSum;
		if(node.left == null && node.right == null){
			System.out.println(newRunningSum);
			sums.add(newRunningSum);
			
		}
		calculateBranchSum(node.left,newRunningSum,sums);
		calculateBranchSum(node.right,newRunningSum,sums);

	}
		
}
```


 Related 


### Takeaways
1.  if+if 可以尝试简化
2.  想要用function 携带信息， 也可以用 加减法实现 sum == 路上的都减去最后相等。
3. use of stack for dfs
4. use of queue for bfs

 