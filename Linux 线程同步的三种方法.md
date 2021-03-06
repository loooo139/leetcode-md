# Linux 线程同步的三种方法

线程的最大特点是资源的共享性，但资源共享中的同步问题是多线程编程的难点。linux下提供了多种方式来处理线程同步，最常用的是**互斥锁**、**条件变量**和**信号量**。

## 一、互斥锁(mutex)
通过锁机制实现线程间的同步。

## 1. 初始化锁:

> 在Linux下，线程的互斥量数据类型是pthread_mutex_t。在使用前,要对它进行初始化。
> 静态分配：`pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER`;
> 动态分配：`int pthread_mutex_init(pthread_mutex_t *mutex, const pthread_mutex_attr_t *mutexattr)`;
> ##2. 加锁:
> 对共享资源的访问，要对互斥量进行加锁，如果互斥量已经上了锁，调用线程会阻塞，直到互斥量被解锁。

```
int pthread_mutex_lock(pthread_mutex *mutex);
int pthread_mutex_trylock(pthread_mutex_t *mutex);
12
```

解锁。在完成了对共享资源的访问后，要对互斥量进行解锁。

```
int pthread_mutex_unlock(pthread_mutex_t *mutex);
1
```

销毁锁。锁在是使用完成后，需要进行销毁以释放资源。

```
int pthread_mutex_destroy(pthread_mutex *mutex);
1
```

# 二、条件变量(cond)
## 1.与互斥锁的区别:

> 与互斥锁不同，条件变量是用来等待而不是用来上锁的。条件变量用来自动阻塞一个线程，直到某特殊情况发生为止。通常条件变量和互斥锁同时使用。条件变量分为两部分: 条件和变量。条件本身是由互斥量保护的。线程在改变条件状态前先要锁住互斥量。条件变量使我们可以睡眠等待某种条件出现。条件变量是利用线程间共享的全局变量进行同步的一种机制，主要包括两个动作：一个线程等待”条件变量的条件成立”而挂起；另一个线程使”条件成立”（给出条件成立信号）。条件的检测是在互斥锁的保护下进行的。如果一个条件为假，一个线程自动阻塞，并释放等待状态改变的互斥锁。如果另一个线程改变了条件，它发信号给关联的条件变量，唤醒一个或多个等待它的线程，重新获得互斥锁，重新评价条件。如果两进程共享可读写的内存，条件变量可以被用来实现这两进程间的线程同步。
> ##2. 初始化条件变量:
> 静态态初始化，`pthread_cond_t cond = PTHREAD_COND_INITIALIER;`
> 动态初始化，`int pthread_cond_init(pthread_cond_t *cond, pthread_condattr_t *cond_attr);`

## 3. 等待条件成立:
释放锁,同时阻塞等待条件变量为真才行。timewait()设置等待时间,仍未signal,返回ETIMEOUT(加锁保证只有一个线程wait)

```
int pthread_cond_wait(pthread_cond_t *cond, pthread_mutex_t *mutex);
int pthread_cond_timewait(pthread_cond_t *cond,pthread_mutex *mutex,const timespec *abstime);
12
```

激活条件变量。`pthread_cond_signal,pthread_cond_broadcast`（激活所有等待线程）

```
int pthread_cond_signal(pthread_cond_t *cond);
1
int pthread_cond_broadcast(pthread_cond_t *cond); //解除所有线程的阻塞
1
```

清除条件变量。无线程等待,否则返回EBUSY

```
int pthread_cond_destroy(pthread_cond_t *cond);
1
```

# 三、信号量(sem)
如同进程一样，线程也可以通过信号量来实现通信，虽然是轻量级的。信号量函数的名字都以”sem_”打头。线程使用的基本信号量函数有四个。

## 1. 信号量初始化:

```
int sem_init (sem_t *sem , int pshared, unsigned int value);
1
```

这是对由sem指定的信号量进行初始化，设置好它的共享选项(linux 只支持为0，即表示它是当前进程的局部信号量)，然后给它一个初始值VALUE。
## 2. 等待信号量:
给信号量减1，然后等待直到信号量的值大于0。

```
int sem_wait(sem_t *sem);
1
```

释放信号量。信号量值加1。并通知其他等待线程。

```
int sem_post(sem_t *sem);
1
```

销毁信号量。我们用完信号量后都它进行清理。归还占有的一切资源。

```
int sem_destroy(sem_t *sem);
```