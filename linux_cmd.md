# 常用指令  
## tar  
解包：tar -xvf filename.tar  
打包：tar -cvf filename.tar dirname  (dirname2 dirname3) 
解包(软链接)：tar -xvf filename.tar git
打包(软链接)：tar -hcvf filename.tar dirname  (dirname2 dirname3)

## zip  
解压：unzip filename.zip  
压缩：zip -r filename.zip dirname  

## rar
解压：unrar e test.rar  
压缩：rar a test.rar test  

## mv 
多文件：mv src1 src2 src3 -t dest  

## ln  
硬链接（同一文件）：ln src dest  
软链接（快捷方式）：ln -s src dest  

## find （查找文件）  
find dirname -name "str"

## grep （查找字符串）  
grep "str" dirname -R

## mkdir  
创建并设置权限：mkdir -m 777 dirname  
创建路径上的目录：mkdir -p rootdir/dirname  

# cp  
-a 该选项通常在拷贝目录时使用。它保留链接、文件属性，并递归地拷贝目录，其作用等于dpr选项的组合  

# useradd  
增加用户: useradd tt
删除用户：userdel -r(同时删除文件) tt
