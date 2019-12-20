# debug_print  
## printk  
```C
//消息级别 
#include <linux/kern_levels.h>
#define KERN_SOH  "\001" 
#define KERN_EMERG KERN_SOH "0"  /* 紧急事件，一般是内核崩溃 */
#define KERN_ALERT KERN_SOH "1"  /* 必须立即采取行动 */
#define KERN_CRIT  KERN_SOH "2"  /* 临界条件，比如严重的软件或硬件错误*/
#define KERN_ERR  KERN_SOH "3"  /* 错误状态，一般设备驱动程序中使用KERN_ERR 报告硬件错误 */
#define KERN_WARNING KERN_SOH "4"  /* 警告信息，不会对系统造成严重影响 */
#define KERN_NOTICE  KERN_SOH "5"  /* 有必要进行提示的一些信息 */
#define KERN_INFO  KERN_SOH "6"  /* 提示性的信息 */
#define KERN_DEBUG KERN_SOH "7"  /* 调试信息 */

#include <linux/printk.h>
#define CONSOLE_LOGLEVEL_DEFAULT 7 /*优先级高于 7 的消息才能显示在控制台上*/  

//printk 不带消息级别将会采用默认级别MESSAGE_LOGLEVEL_DEFAULT 4
printk(KERN_EMERG "gsmi: Log Shutdown Reason\n");

//修改可输出消息级别 
#cat /proc/sys/kernel/printk               //查看printk对应的打印级别
//修改init.rc 
#echo 8 4 1 7 > /proc/sys/kernel/printk    //打开打印
#echo 1 4 1 7 > /proc/sys/kernel/printk    //关闭打印
```

## dev_info/dev_dbg/dev_err    
```c
#include <linux/device.h>

#if defined(CONFIG_DYNAMIC_DEBUG)
#define dev_dbg(dev, format, ...)		     \
do {						     \
	dynamic_dev_dbg(dev, format, ##__VA_ARGS__); \
} while (0)
#elif defined(DEBUG)
#define dev_dbg(dev, format, arg...)		\
	dev_printk(KERN_DEBUG, dev, format, ##arg)
#else
#define dev_dbg(dev, format, arg...)				\
({								\
	if (0)							\
		dev_printk(KERN_DEBUG, dev, format, ##arg);	\
})

//在需要使能dev_dbg的文件顶部 #define DEBUG

```  