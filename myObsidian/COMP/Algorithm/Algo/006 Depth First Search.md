---
aliases: [algo 006 , ]
tags:
  - tree
  - dfs
---
## Algo 006
```java
import java.util.*;
class Program { 
	static class Node {
	    String name;
	    List<Node> children = new ArrayList<Node>();
	    public Node(String name) { 
	        this.name = name;
		}
    // Time: O(v+e) Space: O (v)
	    public List<String> depthFirstSearch(List<String> array) {
	        array.add(this.name);
	        for(int i =0; i<childe.size();i++){
	            children.get(i).depthFirstSearch(array);
	        }
	        return array;
	    }
	    public Node addChild(String name) { 
	        Node child = new Node(name); 
	        children.add(child);
	        return this;
	    }
	}

}
```

#### Takeaways
1. java return this? 

#### Related
