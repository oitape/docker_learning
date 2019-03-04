WrdPress使用MySQL的数据库程序来存储大部分程序，先确保运行WordPress的容器使只读文件系统。
只读文件系统的两个效果
- 你对容器不能更改他所包含的文件
- 容器中的攻击者无法破坏文件

```sh
docker run -d --name wp --read-only wordpress:4
```