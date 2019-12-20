# pinctrl_gpio  

## 功能对比
| gpio             | pinctrl              |
| ---------------- | -------------------- |
| 输入输出高低电平 | 引脚功能MUX          |
| 接收外部中断     | 配置上下拉及驱动能力 |

## 内核api  
### pinctrl
```c
//获取一个pinctrl句柄
struct pinctrl *devm_pinctrl_get(struct device *dev);
//获取这个pin对应pin_state
struct pinctrl_state *pinctrl_lookup_state(struct pinctrl *p, const char *name);
//设置引脚为为某个stata  
int pinctrl_select_state(struct pinctrl *p, struct pinctrl_state *state);
```

### gpio  
#### of api
```c
//获取设备树某个属性里面定义了几个 GPIO 信息，要注意的是空的 GPIO 信息也会被统计到
int of_gpio_named_count(struct device_node *np, const char *propname);
//同上 此函数统计的是“gpios”这个属性的 GPIO 数量
int of_gpio_count(struct device_node *np);
//函数获取 GPIO 编号  
int of_get_named_gpio(struct device_node *np,const char *propname,int index);
```
#### 控制api
```c
int devm_gpio_request(struct device *dev, unsigned gpio, const char *label);
//flags: GPIOF_DIR_OUT/GPIOF_IN
int devm_gpio_request_one(struct device *dev, unsigned gpio,
			  unsigned long flags, const char *label);
void devm_gpio_free(struct device *dev, unsigned int gpio);

static inline int gpio_get_value(unsigned gpio);
static inline void gpio_set_value(unsigned gpio, int value);
```