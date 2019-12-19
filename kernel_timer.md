# kernel_timer  
## jiffies  
```c
unsigned long timeout;
timeout = jiffies + (2 * HZ); /* 超时的时间点 */
/*************************************
具体的代码
************************************/
/* 判断有没有超时 */
if(time_before(jiffies, timeout)) {
    /* 超时发生 */
    } else {
    /* 超时未发生 */
}
```
```c
int jiffies_to_msecs(const unsigned long j) 将 jiffies 类型的参数 j 分别转换为对应的毫秒、微秒、纳秒。
int jiffies_to_usecs(const unsigned long j)
u64 jiffies_to_nsecs(const unsigned long j)
long msecs_to_jiffies(const unsigned int m) 将毫秒、微秒、纳秒转换为 jiffies 类型。  
long usecs_to_jiffies(const unsigned int u)
unsigned long nsecs_to_jiffies(u64 n)
```  

## 内核定时器  
```c
#include <linux/timer.h>
struct timer_list timer; /* 定义定时器 */
/* 定时器回调函数 */
void function(unsigned long arg)
{
    /*
    * 定时器处理代码
    */
    /* 如果需要定时器周期性运行的话就使用 mod_timer
    * 函数重新设置超时值并且启动定时器。
    */
    mod_timer(&dev->timertest, jiffies + msecs_to_jiffies(2));
}

/* 初始化函数 */
void init(void)
{
    init_timer(&timer); /* 初始化定时器 */

    timer.function = function; /* 设置定时处理函数 */
    timer.expires=jffies + msecs_to_jiffies(2);/* 超时时间 2 秒 */
    timer.data = (unsigned long)&dev; /* 将设备结构体作为参数 */

    add_timer(&timer); /* 启动定时器 */
}

/* 退出函数 */
void exit(void)
{
    del_timer(&timer); /* 删除定时器 */
    /* 或者使用 */
    del_timer_sync(&timer);
}
```  

## 内核短延时函数  
```c
void ndelay(unsigned long nsecs) 纳秒、微秒和毫秒延时函数。
void udelay(unsigned long usecs)
void mdelay(unsigned long mseces)
```