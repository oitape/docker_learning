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
