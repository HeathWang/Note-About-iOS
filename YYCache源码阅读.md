# YYCache源码阅读

[YYCache源码解析 - 掘金](https://juejin.im/post/5a657a946fb9a01cb64ee761)

## YYMemoryCache

主要涉及到缓存算法，LRU(least-recently-used) 淘汰算法。
用到了链表。

## 线程安全

* YYMemoryCache 使用了 pthread_mutex 线程锁（互斥锁）来确保线程安全
* YYDiskCache 则选择了更适合它的 dispatch_semaphore。

[YYCache设计思路](https://blog.ibireme.com/2015/10/26/yycache/)

