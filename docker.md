# DockerFile





# 停止所有运行的容器

```
docker stop $(docker ps -aq)
```



# 删除所有的镜像

```
docker rmi $(docker images -aq)
```





# 批量删除运行的容器

```
docker rm $(docker ps -aq)
```





# 映射端口

```
//绑定容器的 8080 端口，并将其映射到本地主机 127.0.0.1 的 80 端口上。
docker run -p 127.0.0.1:80:8080/tcp ubuntu bash 

//将容器的2358端口映射到主机的2358端口，两个端口可以相同
docker run -p 2358:2358 -v E:\Test\httpserver:C:\httpserver -it buildtools2017
```





# 删除容器

```
 docker container prune //清理掉所有处于终止状态的容器
 docker rm -f 1e560fca3906 //1e560fca3906为容器ID
```



# 进入容器

1. docker attach

   ```
   docker attach 1e560fca3906  //如果从这个容器退出，会导致容器的停止
   ```

2. docker exec

   ```
   docker exec -it 243c32535da7 /bin/bash //如果从这个容器退出，不会导致容器的停止
   ```

   

# 重启已经停止的容器

```
docker restart b750bbbcfd88 // docker restart <容器 ID>
```





# 停止一个容器

```
docker stop b750bbbcfd88 // docker stop <容器 ID>
```





# 启动一个已经停止的容器

```
docker start b750bbbcfd88  //b750bbbcfd88为容器ID，可通过docker ps -a 查询
```



# 查看所有容器运行状态

```
docker ps -a
```





# 将本地目录挂载在docker容器中

  docker run -v  本地目录：容器目录

```
docker run -v E:\test\httpserver:C:\httpserver -it buildtools2017:latest
```





# 运行交互式的容器

```
docker run -it ubuntu:15.10 /bin/bash			//ubuntu  容器	
docker run -it windowsserver:latest cmd.exe		//windows 容器
```



# 编译dockerfile文件

1. 使用当前目录的 Dockerfile 创建镜像，标签为 runoob/ubuntu:v1。

   ```
   docker build -t runoob/ubuntu:v1 .  // -t: 镜像的名字及标签，通常 name:tag 或者 name 格式
   ```

   

2. 通过 -f设置 Dockerfile 文件的位置：

   ```
   docker build -f /path/to/a/Dockerfile .
   ```

3. 编译vs2019dockerfile例子

   ```
   docker build -t buildtools2019:latest -m 2GB .
   ```

   



# 查看镜像信息

```
docker images
```





# 修改docker镜像和容器存储位置

```json
{    
    "data-root": "d:\\docker_images_systems"
}
```





# 加载已有镜像

```dockerfile
docker load < busybox.tar.gz
docker load --input fedora.tar
```

