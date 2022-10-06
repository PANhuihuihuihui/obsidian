阻塞队列是一个可以阻塞的先进先出集合，比如某个线程在空队列获取元素时、或者在已存满队列存储元素时，都会被阻塞。

> 说白了就是干等着，啥也干不了。排队上车的时候，你就只能一直站在在那里排队，你要是想去上厕所回来你的位置都不见了，还得重新排队。

BlockingQueue 接口常用的实现类如下：

-   ArrayBlockingQueue ：基于数组的有界阻塞队列，必须指定大小。
-   LinkedBlockingQueue ：**基于单链表的无界阻塞队列，不需指定大小**。
-   PriorityBlockingQueue ：基于最小二叉堆的无界、优先级阻塞队列。
-   DelayQueue：基于延迟、优先级、无界阻塞队列。
-   SynchronousQueue ：基于 CAS 的阻塞队列。