---
aliases: [leetcode 002 ]
tags: 
  - linked-list
  - math
---
## Problem
You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.


#### solution
1. myself
```java
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
	Boolean addon= false,first = true;
	ListNode pre = null,head = null,curr = null;
	while (l1 != null || l2 != null) {
		int x = (l1 != null) ? l1.val : 0;
		int y = (l2 != null) ? l2.val : 0;
		int val = addon ?  x+y +1 : x+y;
		if (val >= 10){
			val = val%10;
			addon = true;
		}
		else {
			addon =false;
		}
		if(first){
			head = new ListNode(val, null);
			pre = head;
			first = false;
		}
		else{
			curr = new ListNode(val, null);
			pre.next = curr;
			pre = curr;
		}

		l1 = (l1 == null) ? null : l1.next;
		l2 = (l2 == null) ? null : l2.next;

	}
	if(addon){
		curr = new ListNode(1, null);
		pre.next = curr;
		pre = curr;
	}
	return head;
        
}
-   1568/1568 cases passed (4 ms)
-   Your runtime beats 38.4 % of java submissions
-   Your memory usage beats 22.04 % of java submissions (48.3 MB)
```
2.  suggest (similar but more consice)
```java
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
	ListNode dummyHead = new ListNode(0);
	ListNode curr = dummyHead;
	int carry = 0;
	while (l1 != null || l2 != null || carry != 0) {
		// better add carry to loop
		int x = (l1 != null) ? l1.val : 0;
		int y = (l2 != null) ? l2.val : 0;
		int sum = carry + x + y;
		carry = sum / 10;
		curr.next = new ListNode(sum % 10);
		curr = curr.next;
		if (l1 != null)
			l1 = l1.next;
		if (l2 != null)
			l2 = l2.next;
	}
	return dummyHead.next;
}
-   1568/1568 cases passed (3 ms)
-   Your runtime beats 80.74 % of java submissions
-   Your memory usage beats 57.87 % of java submissions (47.7 MB)
```
3. 


### Takeaway
Linklist 处理技巧 
1. a.attribute 前一定要判断是a是不是为null
2. curr + pre + next 的关系
3. use of dummy node is helpful

!! 效率 计时做