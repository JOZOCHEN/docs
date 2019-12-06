# 常用指令  
## tar  
解包：tar -zxvf filename.tar  
打包：tar -czvf filename.tar dirname  (dirname2 dirname3)  

## zip  
解压：unzip filename.zip  
压缩：zip -r filename.zip dirname  

## rar
解压：unrar e test.rar  
压缩：rar a test.rar test  

## mv 
多文件：mv src1 src2 src3 -t dest  

## find （查找文件）  
find dirname -name "str"

## grep （查找字符串）  
grep "str" dirname -R
