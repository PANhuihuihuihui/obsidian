---
aliases: [algo 008 , ]
tags:
  - 
---

## Algo 008
#### Solution I Simple recursion
```java
// O(2^n) time | O(n) space
public static int getNthFib1(int n) {
   if(n ==2) return 1;
   else if (n ==1) return 0;
   else return getNthFib1(n-1)+ getNthFib1(n-2);
}
```
注意一下space complex O(N)  因为recursion 就是stack 

#### Solution II Hashmap
```java
// O(n) time | O(n) space
public static int getNthFib(int n) {
	Map<Integer, Integer> memoize = new HashMap<Integer, Integer>(); 
	memoize.put(1, 0);
	memoize.put(2, 1);
	return getNthFib(n, memoize);
}
public static int getNthFib(int n, Map<Integer, Integer> memoize) { 
	if (memoize.containsKey(n)) {
		return memoize.get(n); 
	} else {
		memoize.put(n, getNthFib(n - 1, memoize) + getNthFib(n - 2, memoize));
		return memoize.get(n); 
	}
}
```
存的多，对于多次访问有好处
#### Solution Literative
```java
public static int getNthFib3(int n){
        // literative solution
        if (n == 1) return 0;
        else if (n == 2) return 1;
        else{
            int pprev = 0，prev = 1，curr = 0;
            for(int i= 0;i<n-2;i++){
                curr = pprev+prev;
                pprev = prev;
                prev = curr;    
            }
            return curr;
        } 
    }

public static int getNthFib(int n) {
	int[] lastTwo = {0, 1}; 
	int counter = 3;
	while (counter <= n) {
		int nextFib = lastTwo[0] + lastTwo[1]; 
		lastTwo[0] = lastTwo[1];
		lastTwo[1] = nextFib;
		counter++;
	}
	return n > 1 ? lastTwo[1] : lastTwo[0]; // good
}
```
不存，但是space complextiy 低
#### Takeaways
1. static key in java
2. 