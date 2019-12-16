# printk  
## 消息级别  
```
include/linux/kern_levels.h

#define KERN_SOH  "\001" 
#define KERN_EMERG KERN_SOH "0"  /* 紧急事件，一般是内核崩溃 */
#define KERN_ALERT KERN_SOH "1"  /* 必须立即采取行动 */
#define KERN_CRIT  KERN_SOH "2"  /* 临界条件，比如严重的软件或硬件错误*/
#define KERN_ERR  KERN_SOH "3"  /* 错误状态，一般设备驱动程序中使用
KERN_ERR 报告硬件错误 */
#define KERN_WARNING KERN_SOH "4"  /* 警告信息，不会对系统造成严重影响 */
#define KERN_NOTICE  KERN_SOH "5"  /* 有必要进行提示的一些信息 */
#define KERN_INFO  KERN_SOH "6"  /* 提示性的信息 */
#define KERN_DEBUG KERN_SOH "7"  /* 调试信息 */
```  
```  
 include/linux/printk.h
 #define CONSOLE_LOGLEVEL_DEFAULT 7 /*优先级高于 7 的消息才能显示在控制台上*/
```  
