---
aliases: [ArrayList , LinkList ]
---

# Array
Problem: Fixsize

# ArrayList
All Implemented Interfaces:
Serializable, Cloneable, Iterable\<E\>, Collection\<E\>, List\<E\>, RandomAccess
- size, isEmpty, get, set, iterator, and listIterator O(1)
- The add operation runs in _amortized constant time_
- has a _capacity_.  could be ensureCapacity();
- **not synchronized.**  经常通过包括list 的类来完成，如果没有 Collections.synchronizedList 
- fail-fast 如果for循环中改变的List iterator will throw a ConcurrentModificationException. 注意 这种机制不能用来debug 因为他是best-effort 不保证一定立刻抛出异常。
```java

```
# LinkList
All Implemented Interfaces:
Serializable, Cloneable, Iterable\<E\>, Collection\<E\>, Deque\<E\>, List\<E\>, Queue\<E\>.
- int base operation will self-decided from end or begining.
- **not synchronized.**  Collections.synchronizedList
- fail-fast

