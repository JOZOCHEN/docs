# git&repo    

## git指令  

配置用户名/邮箱：  
git config --global user.name "nameVal"  
git config --global user.email "eamil@qq.com"  

读取用户名/邮箱：  
git config user.name  
git config user.email  

分支管理    
查看：git branch -a(显示远端分支)   
创建：git checkout -b branch_name   
切换：git checkout branch_name  
删除：git branch -d branch_name 

## repo指令
分支管理：  
查看：repo branch   
创建：repo start branch_name --all(对所有工程)  
切换：repo checkout branch_name  
删除：repo abandon branch_name  

对所有工程执行脚本  
repo forall -c 'git checkout branch_name'  

## github  
参考教程 <https://www.liaoxuefeng.com/wiki/896043488029600/900937935629664>

git国内下载站 <https://github.com/waylau/git-for-win>

生成SSH-KEY: ssh-keygen -C "email"


