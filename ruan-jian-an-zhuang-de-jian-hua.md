### 镜像安装细节
- Docker Hub和其他注册服务器
- 使用docker save 和docker load命令加载、导出镜像文件
- 使用Dockerfiles构建镜像

仓库可容纳多个镜像，每个库中的镜像可由标签来唯一标识。
当使用`docker pull` 或 `docker run`命令，如果没有指定一个替代的注册服务器，Docker默认将在Docker Hub里面找。

### 镜像发布的两种方式
 - 使用命令行来发布独立系统构建镜像，这种方式被认为是不能信任的。
 - 公开Dockerfile，并使用Docker Hub的持续构建系统。可信赖的方式。
 
使用私有的Docker Hub注册服务器，或将镜像推送到Docker Hub上你的账号中。需要你的认证授权。使用`docker login`命令登录到Docker'Hub，这样就可以从私有库下载、推送到你控制的任何镜像库。
 运行`docker login`提醒你输入账号密码。完成后使用`docker logout`命令退出。
 
查询想要安装的软件
```sh
docker search <NAME>
```
因为Docker Hub是免费的公共服务，用户会建立大量的个人副本。选择时我们要注意代码是否值得信赖。运行`docker search`可以看到镜像是从公开的脚本构建的，在`AUTOMATED`列寻找一个`[OK]`的标记。

### Docker Hub不是软件的唯一来源
其他安装软件的三种方式：
- 使用替代仓库的注册服务器或运行自己的注册服务器
这种方式需要的视注册服务器的地址，注册服务器后面章节讲解。命令如下
```sh
docker pull quay.io/dockerinaction/ch3_hello_registry:latest
```
格式如下
```
[REGISTRYHOST/][USERNAME/]NAME[:TAG]
```
 
- 可以手动从文件加载镜像
Docker 提供一个命令将镜像由文件加载到Docker。
首先讲下如何保存一个DockerHub中的镜像到本地文件。
```sh
docker pull busybox
docker pull <imageName>
```
然后执行如下保存命令
```sh
docker save -o ~/Desktop/myfile.tar busybox
docker save -o myfile.tar <imageName>
```
你会看到桌面上存在一个myfile.tar的文件。接着运行移除镜像的命令
```sh
docker image rm busybox
或者
docker rmi busybox
```
移除镜像后，使用docker load将创建的文件再次加载。如果运行`docker load`命令而不使用 -i 参数，Docker会使用标准输入流，而不是从文件读取归档。
```sh
docker load -i ~/Desktop/myfile.tar
```
然后使用`docker images`命令你会看到busybox镜像在列表当中。


- 从其他来源下载项目，并利用提供的Dockerfile自检镜像。
分发Dockerfile类似于分发镜像文件。一般常用Git。
```sh
git clone https://github.com/dockerinaction/ch3_dockerfile.git
```
下载完成会看到一个ch3_dockerfile，然后运行如下命令指定ch3_dockerfile路径
``sh
docker build -t dia_ch3/dockerfile ch3_dockerfile
```
然后使用`docker images`命令你会看到dia_ch3/dockerfile镜像在列表当中。























