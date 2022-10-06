---
aliases: leetcode 009
tags:
  - math
---

## Leetcode 009
Given an integer `x`, return `true` if `x` is palindrome integer.
An integer is a **palindrome** when it reads the same backward as forward.
-   For example, `121` is a palindrome while `123` is not.

**Follow-up:** Could you solve it without converting the integer to a string?

#### solution 
1. myself
	注意string 的 length() -1
```java
public boolean isPalindrome(int x) {
        String s = String.valueOf(x);
        for (int i =0;i<s.length()/2; i++){
            if (s.charAt(i) != s.charAt(s.length()-i-1)){
                return false;
            }
        }  
        return true;
    }
11510 / 11510** test cases passed.
Runtime: **9 ms**
Memory Usage: **41.5 MB**
    
```
2.  not converting the integer to a string
```java
public boolean isPalindrome(int x) {
        // 利用位数 % 取余数 / 取整数
        if(x<0|| (x!=0 && x%10 ==0)) return false; // 不能只有小于0 因为我们这里要对10整除所以 还不能被十整除
		int res = 0;
		while(x>res){
			res = res*10+x%10 // 1221 res = 1  >>> res = 10+ 2 = 12
			x = x/10 // 1221 x = 122
		}
		return (x==res || x==res/10)
    }
-   11510/11510 cases passed (15 ms)
-   Your runtime beats 51.05 % of java submissions
-   Your memory usage beats 82.55 % of java submissions (44 MB)
```

#### Take away
how to get the reverse num:  res = res*10+x%10
why string is faster than the num solution? 