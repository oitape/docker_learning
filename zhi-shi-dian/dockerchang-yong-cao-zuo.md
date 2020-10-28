- docker常用命令
<style>
    table th:nth-of-type(1) {  
        width: 130px; 
    }
    table th:nth-of-type(2) {  
        width: 200px; 
    }
</style>
| 作用 | 命令 | 
| :- | :- |
| 搜索 | `docker search ${key}` |
| 拉取镜像 | `docker pull 镜像名:TAG` <br>  `Tag表示版本，有些镜像的版本显示latest，为最新版本`|
|查看所有镜像| `docker images ls`|
|删除镜像|`docker rmi -f 镜像ID或者镜像名:TAG` <br> `-f 表示强制删除`|
|获取源信息|`docker inspect 镜像ID或者镜像名:TAG`|
|运行|`docker run --name 容器名 -i -t -p 主机端口:容器端口 -d -v 主机目录:容器目录:ro 镜像ID或镜像名:TAG` <br> `--name 指定容器名，可自定义，不指定自动命名` <br> `-i 以交互模式运行容器` <br> `-t 分配一个伪终端，即命令行，通常-it组合来使用` <br> `-p 指定映射端口，讲主机端口映射到容器内的端口`<br>`-d 后台运行容器` <br> `-v 指定挂载主机目录到容器目录，默认为rw读写模式，ro表示只读` |
|容器列表|`docker ps -a -q` <br> `-a 查看所有容器(运行中、未运行)` <br> `-q 只查看容器的ID`|
|容器操作|`docker start 容器ID或容器名`<br>`docker stop 容器ID或容器名`<br> ` docker rm -f 容器ID或容器名`|
|容器日志|`docker logs 容器ID或容器名`|
|进入容器|`docker exec -it 容器ID或者容器名 /bin/bash`|
|copy文件|` docker cp 主机文件路径 容器ID或容器名:容器路径 #主机中文件拷贝到容器中` <br> `docker cp 容器ID或容器名:容器路径 主机文件路径 #容器中文件拷贝到主机中`|
|容器元信息|`docker inspect 容器ID或容器名`|

