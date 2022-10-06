---
aliases: [Stack , Queue ]
---

# Stack
All Implemented Interfaces: Serializable, Cloneable, Iterable\<E\>, Collection\<E\>, List\<E\>, RandomAccess

It extends class Vector with five operations that allow a vector to be treated as a stack.
`empty() peek() pop() search()`
Related from [[Vector]] (base) to [[Deque]] (complete and consistent)

# Queue
**All Superinterfaces**: Collection\<E\>, Iterable\<E\>
**All Known Subinterfaces**: BlockingDeque\<E\>, [[BlockingQueue]]\<E\>, [[Deque]]\<E\>, TransferQueue\<E\>
**All Known Implementing Classes:**
AbstractQueue, ArrayBlockingQueue, ArrayDeque, 
ConcurrentLinkedDeque, ConcurrentLinkedQueue, DelayQueue, LinkedBlockingDeque, LinkedBlockingQueue, LinkedList, LinkedTransferQueue, PriorityBlockingQueue, [[PriorityQueue]], SynchronousQueue
- methods exsits in two form: 1. return fasle or null 2. throw expection
	原因: is designed for use when failure is a normal eg: **fixed-capacity** 
| ---        | _Throws exception_ | _Returns special value_ |
| ---------- | ------------------ | ----------------------- |
| **Insert** | `add(e)`             | `offer(e)`                |
| **Remove** | `remove(e)`           | `poll(e)`                  |
| **Examine**    | `element(e)`          | `peek(e)`                  |
- _blocking queue methods_  in concurrent case see [[BlockingQueue]]
- not allow `null`  in the queue because it is the return value of the `offer(e)` and `poll(e)`

Java中的Queue的实现有三种方式：
-   阻塞队列
-   非阻塞队列
-   双向队列