WrdPress使用MySQL的数据库程序来存储大部分程序，先确保运行WordPress的容器使只读文件系统。
只读文件系统的两个效果
- 你对容器不能更改他所包含的文件
- 容器中的攻击者无法破坏文件

```sh
docker run -d --name wp --read-only wordpress:4
```
可以通过检查容器元数据查看容器是否在运行,如果在运行输出为真。
```sh
docker inspect --format "{{.State.Running}}" wp
```

会报错，WordPress 有一个MySQL的数据库依赖关系
```sh
docker run -d --name wpdb -e MYSQL_ROOT_PASSWORD=ch2demo mysql:5
```

再次执行如下命令(修改原书命令，增加 -v /tmp/，解决依旧报错问题)
```sh
docker run -d --name wp2 --read-only -v /run/lock/apache2/ -v /run/apache2/ -v /tmp/ --link wpdb:mysql -p 80 wordpress:4
```
再通过检查容器元数据发现成功运行中了。
通过使用只读文件系统，以及链接WordPress到另一个运行着数据库的容器，可以确保运行WordPress镜像的容器永远不会改变，如果客户的WP机器除了问题，可在其他地方启动该容器的另一个副本。

目前这样做还是有两个问题
- MySQL和WP运行在同一台机器上
- WP对重要的设置：数据库名称、管理用户、管理密码数据库加盐等使用默认值。解决这个问题可以创建多个版本WP软件，每个客户特殊配置。
通过环境变量来注入配置则是一个更好的方式。