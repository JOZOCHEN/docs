# shell_script  

参考：<https://www.runoob.com/linux/linux-shell.html>  
操作文件: <https://blog.csdn.net/qq_37674858/article/details/80066264>  
截取给定路径中的目录部分:<https://www.cnblogs.com/kevingrace/p/6182573.html>  

## 根据进程名结束进程：
ps -ef | grep procedure_name | grep -v grep | awk '{print $2}' | xargs kill -2
