# docker  
## cmd
创建容器（共享文件夹）:docker run -it (ubuntu) bash   
为已创建容器增加运行参数：docker container update (option) (container_id)    
参数：   
指定容器名称：--name (container_name)  
设置共享文件夹：-v (local_path/file):(/dest_path/file)  
拥有真root权限(可执行mount): --privileged 

删除容器: docker rm (container_id) 

修改容器名: docker rename (old_name) (new_name)

启动容器：docker start (container_id)  
停止容器: docker stop (container_id)  

进入容器：docker exec -it (container_id) bash  
退出容器：ctrl+d    

