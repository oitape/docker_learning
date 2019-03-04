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