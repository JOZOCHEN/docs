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

## OF函数  
### 查找节点
```c
//直接获取当前设备根节点
const struct device_node *np = priv->dev->dev.of_node; 
//通过节点名字查找指定的节点
struct device_node *of_find_node_by_name(struct device_node *from,
                                        const char *name); 
//通过 device_type 属性查找指定的节点
struct device_node *of_find_node_by_type(struct device_node *from, 
                                        const char *type); 
//根据 device_type 和 compatible 这两个属性查找指定的节点
struct device_node *of_find_compatible_node(struct device_node *from,const char *type, 
                                            const char compatible); 
//通过 of_device_id 匹配表来查找指定的节点
struct device_node *of_find_matching_node_and_match(struct device_node *from, 
                                const struct of_device_id *matches,const struct of_device_id **match); 
//通过路径来查找指定的节点
struct device_node *of_find_node_by_path(const char *path); 
```
### 查找父/子节点  
```c
//获取指定节点的父节点
struct device_node *of_get_parent(const struct device_node *node);  
//迭代的查找子节点
struct device_node *of_get_next_child(const struct device_node *node, struct device_node *prev); 

```

### 提取属性值  
```c
//查找指定的属性
property *of_find_property(const struct device_node *np, const char *name, int *lenp);
//获取属性中元素的数量
int of_property_count_elems_of_size(const struct device_node *np,const char *propname,int elem_size);
//从属性中获取指定标号的 u32 类型数据值,如某个属性有多个 u32 类型的值，那么就可以使用此函数来获取指定标号的数据值
int of_property_read_u32_index(const struct device_node *np,const char *propname,
                                u32 index,u32 *out_value);
//连续读取属性中 u8、u16、u32 和 u64
int of_property_read_u8_array(const struct device_node *np,const char *propname,u8 *out_values,size_t sz);
//读取只有一个 u8、u16、u32 和 u64 整形值的属性
int of_property_read_u8(const struct device_node *np, const char *propname, u8 *out_value);
//读取属性中字符串值  
int of_property_read_string(struct device_node *np,const char *propname,const char **out_string);
//获取#address-cells 属性值  
int of_n_addr_cells(struct device_node *np); 
//获取#size-cells 属性值
int of_n_size_cells(struct device_node *np);
```

### 其他常用
```c
//于查看节点的 compatible 属性是否有包含 compat 指定的字符串，也就是检查设备节点的兼容性
int of_device_is_compatible(const struct device_node *device,const char *compat);
//用于获取地址相关属性，主要是“reg”或者“assigned-addresses”属性值
const __be32 *of_get_address(struct device_node *dev,int index,u64 *size,unsigned int *flags);
//将从设备树读取到的地址转换为物理地址
u64 of_translate_address(struct device_node *dev,const __be32 *in_addr);
//将reg 属性值转换为 resource 结构体类型
int of_address_to_resource(struct device_node  *dev,int index,struct resource *r);
//获取内存地址所对应的虚拟地址  
void __iomem *of_iomap(struct device_node *np,int index);
```
### gpio相关
```c
//获取设备树某个属性里面定义了几个 GPIO 信息，要注意的是空的 GPIO 信息也会被统计到
int of_gpio_named_count(struct device_node *np, const char *propname);
//同上 此函数统计的是“gpios”这个属性的 GPIO 数量
int of_gpio_count(struct device_node *np);
//函数获取 GPIO 编号  
int of_get_named_gpio(struct device_node *np,const char *propname,int index);
```
