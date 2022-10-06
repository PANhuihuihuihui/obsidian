# Deque
All Superinterfaces: Collection\<E\>, Iterable\<E\>, Queue\<E\>
`double end queue` 

Deque 是一个既可以在头部操作元素，又可以为尾部操作元素，俗称为双向（双端）队列。Deque 继承自 Queue，Deque 实现类有 LinkedList、 ArrayDeque、ConcurrentLinkedDeque 等等。在将List篇的时候，里面就说LinkedList是一种双向队列，其实它也是Deque的一种实现方式。


常用双向对垒的实现类有：

-   LinkedList：基于单链表的无界双端队列，允许元素为 null。
-   ArrayDeque：基于数组的有界双端队列，不允许 null。不是线程安全的。当作为栈使用时，性能比Stack好；当作为队列使用时，性能比LinkedList好。
