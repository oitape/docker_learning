##从容器构建镜像
### 打包一个HelloWorld
从一个容器构建一个镜像包含三部分：
- 需要从一个已存在的镜像创建一个容器
- 修改这个容器的文件系统，这些改动会被保存在容器的联合文件系统(UFS)的新文件层
- 需要对改动进行提交，这样就能从新镜像创建新的容器

利用下面的简单示例创建一个hw_image的新镜像
1、修改容器中的文件
```sh
docker run --name hw_container ubuntu:latest touch /HelloWorld
```
2、将改动提交到新镜像中
```sh
docker commit hw_container hw_image
\#取出被改动的文件
docker rm -vf hw_container 
```
3、检测容器中的文件
```sh
docker run --rm hw_image ls -l /HelloWorld
```