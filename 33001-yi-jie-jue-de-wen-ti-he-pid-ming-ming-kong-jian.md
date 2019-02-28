#### 什么是PID
每一个运行的程序或进程，在Linux中都有唯一一个编号，叫做进程标识符即PID。
一个PID命名空间是一组识别进程的数字。Linux提供了工具可以创建多个PID命名空间，每个命名空间拥有一套完整的PID，每个PID命名空间将包含自己的PID1、2、3，以此类推。
运行如下命令可以看到:
```sh
 docker run -d --name namespaceA busybox:latest /bin/sh -c 'sleep 30000'
 
 docker run -d --name namespaceB busybox:latest /bin/sh -c 'sleep 30000'
```
运行 ```docker exec namespaceA ps```
> PID   USER     TIME  COMMAND
    1   root      0:00 sleep 30000
   13   root      0:00 ps

运行 ```docker exec namespaceB ps```
> PID   USER     TIME  COMMAND
    1   root      0:00 sleep 30000
    6   root      0:00 ps

使用```docker exec```命令可以在运行的容器中运行额外的进程。`ps` 命令显示所有正在运行的进程和它们的PID。
如果没有PID命令空间，在一个容器内运行的进程将和其他容器或主机共享相同的ID空间，这样，容器无法确定其他主机有哪些进程在运行。
你可以有选择的创建没有PID命名空间的容器。可以通过
`docker create` 或 `dcoker run`中设置 `--pid` 标志以及将该值设置为 `host`来进行尝试.

> 注：常见的冲突问题
 - 两个程序都想要绑定到同一个端口
 - 两个程序都使用相同的临时文件名和文件锁
 - 两个程序想要使用不同版本且全局已经安装的库
 - 同一个程序的两个副本要使用相同的PID文件
 - 第二个安装的程序修改了另一个程序正在使用的环境变量，导致程序的中断
 
Docker通过Linux的命名空间、根文件系统和虚拟网络组件等工具解决了这些软件冲突。所有这些工具都用来为每个容器提供隔离。