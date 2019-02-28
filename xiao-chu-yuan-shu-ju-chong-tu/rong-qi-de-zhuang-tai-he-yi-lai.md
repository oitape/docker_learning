- docker总共有四种状态
    - 运行中
    - 暂停中
    - 重新启动总
    - 已退出
    
 那些被`docker create`创建的容器从未启动(已退出状态)，想看到所有运行ing 或者  退出的容器，使用该命令查看
 ```sh
 docker ps -a
 ```
 如果你要启动已经停掉的容器可以采用如下命令
 ```sh
 docker start <containerID or containerName>
 ```
 
- docker 的链接内在机理
链接的机制将IP地址注入所依赖的容器，在运行的容器中得到该IP地址。如果你尝试启动一个容器，其依赖于另一个并未运行的容器，docker将不会把该容器的IP地址注入到未运行的容器中。
 