# device_tree  
## 属性  
```c
#address-cells /*决定了子节点 reg 属性中地址信息所占用的字长*/  
#size-cells    /*属性值决定了子节点 reg 属性中长度信息所占的字长*/
reg = <address1 length1 address2 length2 address3 length3……> 
/*reg 属性一般用于描述设备地址空间资源信息，一般都是某个外设的寄存器地址范围信息*/

ranges = <0x0 0xe0000000 0x00100000>; /*子地址、父地址和地址空间长度*/
/*此属性值指定了一个 1024KB(0x00100000)的地址范围，子地址空间的物理起始地址为 0x0，父地址空间的物理起始地址为 0xe0000000。*/
ranges; /*子空间和父空间地址范围相同*/

aliases {can0 = &flexcan1;}; /*定义别名*/  
chosen {stdout-path = &uart1;}; /*uboot 向 Linux 内核传递数据*/
```  
