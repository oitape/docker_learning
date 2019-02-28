- 正在运行容器查看
```sh
docker ps
```
类似下面的信息
>CONTAINER ID        IMAGE                       COMMAND                  CREATED             STATUS              PORTS               NAMES
6328d9ca7c6b        dockerinaction/ch2_agent    "/watcher/watcher.sh"    6 minutes ago       Up 5 minutes                            agent

    - 容器ID
    - 使用的镜像
    - 容器中执行的命令
    - 容器运行时长
    - 容器暴露的网络端口
    - 容器名称
    
- 重启容器
```sh
docker restart <containerName or containerID>
```

- 查看日志
```sh
docker logs <containerName or containerID>
```
> docker logs 命令有一个选项，--follow 或者 -f ,用来显示整个日志,容器中日志的变化将实时在终端当中呈现。


- 测试当web服务器停止时会不会发出通知。
    ```sh
    docker stop web
    ```
等待几秒钟，执行
```sh
docker logs mailer
```
如果看到终端输出
>Sending email: To: admin@work  Message: The service is down!

 说明监控成功检测到Web同期中NGINX服务器已经停止。











































































