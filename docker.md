# docker  
## cmd
创建容器（共享文件夹）:docker run --name (container_name) -it -v (/local_path/file):(/dest_path/file) (ubuntu) /bin/bash   
修改容器名: docker rename (old_name) (new_name)

启动容器：docker start (container_id)  
停止容器: docker stop (container_id)  

进入容器：docker exec -it (container_id) /bin/bash  
退出容器：ctrl+d    

