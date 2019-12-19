# concurrency&competition  

## 原子操作  
**32位atomic_t 64位atomic64_t**  
```C
ATOMIC_INIT(int i)  定义原子变量的时候对其初始化。  
int atomic_read(atomic_t *v)  读取 v 的值，并且返回。  
void atomic_set(atomic_t *v, int i)  向 v 写入 i 值。  
void atomic_add(int i, atomic_t *v)  给 v 加上 i 值。  
void atomic_sub(int i, atomic_t *v)  从 v 减去 i 值。  
void atomic_inc(atomic_t *v)  给 v 加 1，也就是自增。  
void atomic_dec(atomic_t *v)  从 v 减 1，也就是自减  
int atomic_dec_return(atomic_t *v)  从 v 减 1，并且返回 v 的值。  
int atomic_inc_return(atomic_t *v)  给 v 加 1，并且返回 v 的值。  
int atomic_sub_and_test(int i, atomic_t *v)  从 v 减 i，如果结果为 0 就返回真，否则返回假  
int atomic_dec_and_test(atomic_t *v)  从 v 减 1，如果结果为 0 就返回真，否则返回假  
int atomic_inc_and_test(atomic_t *v) 给 v 加 1，如果结果为 0 就返回真，否则返回假  
int atomic_add_negative(int i, atomic_t *v)  给 v 加 i，如果结果为负就返回真，否则返回假    

void set_bit(int nr, void *p)  将 p 地址的第 nr 位置 1。  
void clear_bit(int nr,void *p)  将 p 地址的第 nr 位清零。  
void change_bit(int nr, void *p)  将 p 地址的第 nr 位进行翻转。  
int test_bit(int nr, void *p)  获取 p 地址的第 nr 位的值。  
int test_and_set_bit(int nr, void *p)  将 p 地址的第 nr 位置 1，并且返回 nr 位原来的值。  
int test_and_clear_bit(int nr, void *p)  将 p 地址的第 nr 位清零，并且返回 nr 位原来的值。  
int test_and_change_bit(int nr, void *p)  将 p 地址的第 nr 位翻转，并且返回 nr 位原来的值。  
```
## 锁
### 自旋锁  
**自旋锁适用于短时期的轻量级加锁**  
自旋锁API函数适用于SMP或支持抢占的单CPU下线程之间的并发访问，也就是用于线程与线程之间，被自旋锁保护的临界区一定不能调用任何能够引起睡眠和阻塞的API 函数，否则的话会可能会导致死锁现象的发生。
```C
DEFINE_SPINLOCK(spinlock_t lock)  定义并初始化一个自选变量。  
int spin_lock_init(spinlock_t *lock)  初始化自旋锁。  
void spin_lock(spinlock_t *lock)  获取指定的自旋锁，也叫做加锁。  
void spin_unlock(spinlock_t *lock)  释放指定的自旋锁。  
int spin_trylock(spinlock_t *lock)  尝试获取指定的自旋锁，如果没有获取到就返回0。  
int spin_is_locked(spinlock_t *lock) 检查指定的自旋锁是否被获取，如果没有被获取就返回非 0，否则返回 0。    

void spin_lock_irq(spinlock_t *lock)  禁止本地中断，并获取自旋锁。  
void spin_unlock_irq(spinlock_t *lock)  激活本地中断，并释放自旋锁。  
void spin_lock_irqsave(spinlock_t *lock,unsigned long flags) 保存中断状态，禁止本地中断，并获取自旋锁。  
void spin_unlock_irqrestore(spinlock_t*lock, unsigned long flags)将中断状态恢复到以前的状态，并且激活本地中断，释放自旋锁。  

void spin_lock_bh(spinlock_t *lock)  关闭下半部，并获取自旋锁。  
void spin_unlock_bh(spinlock_t *lock)  打开下半部，并释放自旋锁。  
```
**一般在线程中使用 spin_lock_irqsave/spin_unlock_irqrestore，在中断中使用 spin_lock/spin_unlock**  
```C
DEFINE_SPINLOCK(lock) /* 定义并初始化一个锁 */

/* 线程 A */
void functionA (){
    unsigned long flags; /* 中断状态 */
    spin_lock_irqsave(&lock, flags) /* 获取锁 */
    /* 临界区 */
    spin_unlock_irqrestore(&lock, flags)  /* 释放锁 */
}

/* 中断服务函数 */
void irq() {
    spin_lock(&lock) /* 获取锁 */
    /* 临界区 */
    spin_unlock(&lock) /* 释放锁 */
}
```  

### 读写自旋锁  
读写自旋锁为读和写操作提供了不同的锁，一次只能允许一个写操作，也就是只能一个线
程持有写锁，而且不能进行读操作。但是当没有写操作的时候允许一个或多个线程持有读锁，
可以进行并发的读操作。  
```C
DEFINE_RWLOCK(rwlock_t lock)  定义并初始化读写锁  
void rwlock_init(rwlock_t *lock) 初始化读写锁。  
void read_lock(rwlock_t *lock)  获取读锁。  
void read_unlock(rwlock_t *lock)  释放读锁。  
void read_lock_irq(rwlock_t *lock)  禁止本地中断，并且获取读锁。  
void read_unlock_irq(rwlock_t *lock)  打开本地中断，并且释放读锁。  
void read_lock_irqsave(rwlock_t *lock,unsigned long flags) 保存中断状态，禁止本地中断，并获取读锁。  
void read_unlock_irqrestore(rwlock_t *lock,unsigned long flags) 将中断状态恢复到以前的状态，并且激活本地
中断，释放读锁。  
void read_lock_bh(rwlock_t *lock)  关闭下半部，并获取读锁。  
void read_unlock_bh(rwlock_t *lock)  打开下半部，并释放读锁。  
void write_lock(rwlock_t *lock)  获取读锁。  
void write_unlock(rwlock_t *lock)  释放读锁。  
void write_lock_irq(rwlock_t *lock)  禁止本地中断，并且获取读锁。  
void write_unlock_irq(rwlock_t *lock)  打开本地中断，并且释放读锁。  
void write_lock_irqsave(rwlock_t *lock,unsigned long flags) 保存中断状态，禁止本地中断，并获取读锁。  
void write_unlock_irqrestore(rwlock_t *lock,unsigned long flags) 将中断状态恢复到以前的状态，并且激活本地
中断，释放读锁。  
void write_lock_bh(rwlock_t *lock)  关闭下半部，并获取读锁。  
void write_unlock_bh(rwlock_t *lock)  打开下半部，并释放读锁。  
``` 

### 顺序锁  
使用顺序锁的话可以允许在写的时候进行读操作，也就是实现同时读写，但是不允许同时进行并发的写操作。  
```C
DEFINE_SEQLOCK(seqlock_t sl)  定义并初始化顺序锁  
void seqlock_init(seqlock_t *sl)  初始化顺序锁。  
void write_seqlock(seqlock_t *sl)  获取写顺序锁。  
void write_sequnlock(seqlock_t *sl)  释放写顺序锁。  
void write_seqlock_irq(seqlock_t *sl)  禁止本地中断，并且获取写顺序锁  
void write_sequnlock_irq(seqlock_t *sl)  打开本地中断，并且释放写顺序锁。  
void write_seqlock_irqsave(seqlock_t *sl,unsigned long flags)保存中断状态，禁止本地中断，并获取写顺序
锁。  
void write_sequnlock_irqrestore(seqlock_t *sl,unsigned long flags)将中断状态恢复到以前的状态，并且激活本地
中断，释放写顺序锁。  
void write_seqlock_bh(seqlock_t *sl)  关闭下半部，并获取写读锁。  
void write_sequnlock_bh(seqlock_t *sl)  打开下半部，并释放写读锁。  
unsigned read_seqbegin(const seqlock_t *sl)读单元访问共享资源的时候调用此函数，此函数会返回顺序锁的顺序号。  
unsigned read_seqretry(const seqlock_t *sl,unsigned start)读结束以后调用此函数检查在读的过程中有没有对资源进行写操作，如果有的话就要重读。  
``` 

## 信号量  
1. 因为信号量可以使等待资源线程进入休眠状态，因此适用于那些占用资源比较久的场合。  
2. 因此信号量不能用于中断中，因为信号量会引起休眠，中断不能休眠。  
3. 如果共享资源的持有时间比较短，那就不适合使用信号量了，因为频繁的休眠、切换线程引起的开销要远大于信号量带来的那点优势。  
```C
DEFINE_SEAMPHORE(name)  定义一个信号量，并且设置信号量的值为 1。  
void sema_init(struct semaphore *sem, int val)  初始化信号量 sem，设置信号量值为 val。  
void down(struct semaphore *sem)获取信号量，因为会导致休眠，因此不能在中断中使用。  
int down_trylock(struct semaphore *sem);尝试获取信号量，如果能获取到信号量就获取，并且返回 0。如果不能就返回非 0，并且不会进入休眠。  
int down_interruptible(struct semaphore *sem)获取信号量，和 down 类似，只是使用 down 进入休眠状态的线程不能被信号打断。而使用此函数进入休眠以后是可以被信号打断的。  
void up(struct semaphore *sem)  释放信号量  
```  
```C
#include <linux/semaphore.h>  
struct semaphore sem; /* 定义信号量 */
sema_init(&sem, 1)； /* 初始化信号量 */
down(&sem); /* 申请信号量 */
/* 临界区 */
up(&sem); /* 释放信号量 */
```  

## 互斥体  
1. mutex 可以导致休眠，因此不能在中断中使用 mutex，中断中只能使用自旋锁。
2. 和信号量一样，mutex 保护的临界区可以调用引起阻塞的 API 函数。
3. 因为一次只有一个线程可以持有 mutex，因此，必须由 mutex 的持有者释放 mutex。并且 mutex 不能递归上锁和解锁。
```C
DEFINE_MUTEX(name)  定义并初始化一个 mutex 变量。  
void mutex_init(mutex *lock)  初始化 mutex。  
void mutex_lock(struct mutex *lock)获取 mutex，也就是给 mutex 上锁。如果获取不到就进休眠。  
void mutex_unlock(struct mutex *lock)  释放 mutex，也就给 mutex 解锁。  
int mutex_trylock(struct mutex *lock)尝试获取 mutex，如果成功就返回 1，如果失败就返回 0。  
int mutex_is_locked(struct mutex *lock)判断 mutex 是否被获取，如果是的话就返回1，否则返回 0。  
int mutex_lock_interruptible(struct mutex *lock)使用此函数获取信号量失败进入休眠以后可以被信号打断。  
```  

```C
struct mutex lock; /* 定义一个互斥体 */
mutex_init(&lock); /* 初始化互斥体 */
mutex_lock(&lock); /* 上锁 */
/* 临界区 */
mutex_unlock(&lock); /* 解锁 */
``` 

