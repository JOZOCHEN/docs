# source update  

## ubuntu  
修改 /etc/apt/sources.list 在最前面增加源  
更新源 apt-get update  
升级软件 apt-get upgrade    
```shell
#阿里
deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse  
deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse  
deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse  
deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse  
deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse  
#deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse  
#deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse  
#deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse  
#deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse  
#deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse  

#中科大  
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse  
#deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse  
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse  
#deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse  
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse  
#deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse  
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse  
#deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse  
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse  
#deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse  

#163  
deb http://mirrors.163.com/ubuntu/ bionic main restricted universe multiverse  
deb http://mirrors.163.com/ubuntu/ bionic-security main restricted universe multiverse  
deb http://mirrors.163.com/ubuntu/ bionic-updates main restricted universe multiverse  
deb http://mirrors.163.com/ubuntu/ bionic-proposed main restricted universe multiverse  
deb http://mirrors.163.com/ubuntu/ bionic-backports main restricted universe multiverse  
#deb-src http://mirrors.163.com/ubuntu/ bionic main restricted universe multiverse  
#deb-src http://mirrors.163.com/ubuntu/ bionic-security main restricted universe multiverse  
#deb-src http://mirrors.163.com/ubuntu/ bionic-updates main restricted universe multiverse  
#deb-src http://mirrors.163.com/ubuntu/ bionic-proposed main restricted universe multiverse  
#deb-src http://mirrors.163.com/ubuntu/ bionic-backports main restricted universe multiverse  

#清华  
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse  
#deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse  
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse  
#deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse  
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse  
#deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse  
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse  
#deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse  
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse  
#deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse  
```

## debian
修改 /etc/apt/sources.list 在最前面增加源  
更新源 apt-get update  
升级软件 apt-get upgrade    
```shell
#网易
deb http://mirrors.163.com/debian/ stretch main non-free contrib
deb http://mirrors.163.com/debian/ stretch-updates main non-free contrib
deb http://mirrors.163.com/debian/ stretch-backports main non-free contrib
#deb-src http://mirrors.163.com/debian/ stretch main non-free contrib
#deb-src http://mirrors.163.com/debian/ stretch-updates main non-free contrib
#deb-src http://mirrors.163.com/debian/ stretch-backports main non-free contrib
deb http://mirrors.163.com/debian-security/ stretch/updates main non-free contrib
#deb-src http://mirrors.163.com/debian-security/ stretch/updates main non-free contrib

#清华大学更新源
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ stretch main contrib non-free
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ stretch main contrib non-free
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ stretch-updates main contrib non-free
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ stretch-updates main contrib non-free
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ stretch-backports main contrib non-free
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ stretch-backports main contrib non-free
deb https://mirrors.tuna.tsinghua.edu.cn/debian-security stretch/updates main contrib non-free
# deb-src https://mirrors.tuna.tsinghua.edu.cn/debian-security stretch/updates main contrib non-free
```