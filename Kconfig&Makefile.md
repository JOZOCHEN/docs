# Kconfig&Makefile  
## 功能  
|Kconfig|Makefile|
|---|---|
|决定menuconfig中的选项并最终影响Makefile的行为|根据menuconfig的配置决定实际编译的obj文件|

## 语法  
### Kconfig  
```
menu "TEST driver"      #menuconfig中增加子菜单 TEST driver
comment "TEST driver"   #可选 在子菜单选项中增加一行注释

config  TEST  #决定Makefile中的宏定义值，这里为 CONFIG_TEST

    tristate  " TEST support "  #menuconfig中的选项名称, tristate可选为m

    default    y        #该选项的默认值 n（不选择） y（选择） m（编译为ko） 

    depends    on FOO   #FOO被选择后TEST才可以被选择

    select     BAR      #如果TEST被选择则同时选中BAR

    help  
        XXX.  # 对选项的详细描述

endmenu   #匹配 menu
```
### Makefile  
```
obj-$(CONFIG_TEST) += test.o    #若TEST support被选择为y(m)，则将test.c编译为test.o(test.ko)

obj-$(CONFIG_DIR)  += dir/      #若DIR相关项被选择为y，则编译时进入子目录dir寻找子目录Makefile   

obj-$(CONFIG_FOO)  += foo.o     #若FOO相关项被选择为y(m)，则将foo1.c foo2.c 编译为 foo.o(foo.ko)
foo-objs := foo1.o \
            foo2.o \  
```


## 在子目录中增加驱动  
假设目录结构如下:  
- drivers/  
  - dir1/  
    - Kconfig(1) 
    - Makefile(1)  
    - dir2/  
      - Kconfig(2)  
      - Makefile(2)    

在 drivers/dir1 下：  
修改Kconfig(1)  
```
source "drivers/dir1/dir2/Kconfig"    #解析dir1下Kconfig时引入dir2下的Kconfig
```  

修改 Makefile(1) 下：
```
obj-$(CONFIG_TEST) += dir2/
```

在 drivers/dir1/dir2 下：
修改Kconfig(2)
```
menu "TEST driver"
comment "TEST driver"

config TEST
    tristate "test support"

endmenu
```  

修改Makefile(2)  
```
obj-$(CONFIG_TEST) += test.o  
```