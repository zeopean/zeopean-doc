
### Queue 的分类
```
class Queue.Queue(maxsize=0)            #构造一个FIFO队列。

class Queue.LifoQueue(maxsize=0)        #构造一个LIFO队列。

class Queue.PriorityQueue(maxsize=0)    #构造一个优先队列

exception Queue.Empty


exception Queue.Full

```

### Queue 的公共方法

```

Queue.qsize()¶
返回队列的近似大小。注意，队列大小大于0并不保证接下来的get()调用不会被阻塞，
队列大小小于maxsize也不保证接下来的put()调用不会被阻塞。

Queue.empty()
如果队列为空返回True，否则返回False。如果empty()返回True并不保证接下来的put()调用不会被阻塞。
类似的，如果empty()返回False也不能保证接下来的get()调用不会被阻塞。

Queue.full()
如果队列是满的返回True，否则返回False。如果full()返回True并不能保证接下来的get()调用不会被阻塞。类似的，如果full()返回False并不能保证接下来的put()调用不会被阻塞。

Queue.put(item[, block[, timeout]])
将item放入队列中。如果可选的参数block为真且timeout为空对象（默认的情况，阻塞调用，无超时）
，如有必要（比如队列满），阻塞调用线程，直到有空闲槽可用。
如果timeout是个正整数，阻塞调用进程最多timeout秒，如果一直无空闲槽可用，抛出Full异常（带超时的阻塞调用）。如果block为假，如果有空闲槽可用将数据放入队列，否则立即抛出Full异常（非阻塞调用，timeout被忽略）。



Queue.put_nowait(item)
等同于put(item, False)（非阻塞调用）。

Queue.get([block[, timeout]])
从队列中移除并返回一个数据。如果可选的参数block为真且timeout为空对象（默认的情况，阻塞调用，无超时），阻塞调用进程直到有数据可用。
如果timeout是个正整数，阻塞调用进程最多timeout秒，如果一直无数据可用，抛出Empty异常（带超时的阻塞调用）。
如果block为假，如果有数据可用返回数据，否则立即抛出Empty异常（非阻塞调用，timeout被忽略）。



Queue.get_nowait()
等同于get(False)（非阻塞调用）。


# **为了跟踪入队任务被消费者线程完全的处理掉，Queue对象提供了两个额外的方法。**

Queue.task_done()
意味着之前入队的一个任务已经完成。由队列的消费者线程调用。每一个get()调用得到一个任务，
接下来的task_done()调用告诉队列该任务已经处理完毕。

如果当前一个join()正在阻塞，它将在队列中的所有任务都处理完时恢复执行
（即每一个由put()调用入队的任务都有一个对应的task_done()调用）。

如果该方法被调用的次数多于被放入队列中的任务的个数，ValueError异常会被抛出。



Queue.join()
阻塞调用线程，直到队列中的所有任务被处理掉


```