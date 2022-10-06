非阻塞队列是使用**CAS（compare and set）**机制实现，类似 volatile，并发性能好。

> 人太多了，很多现在开始流行取号，先取个号，看着离我这号太远了，我出去溜达溜达一下再来。

常用的阻塞队列有 PriorityQueue 和 ConcurrentLinkedQueue。

-   PriorityQueue ：基于优先级的无界优先级队列
-   ConcurrentLinkedDeque：基于双向链表结构的无界并发队列。