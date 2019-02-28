- 创建多个NGINX容器副本
```sh
docker run -d --name webid nginx
```
如果你复制上面命令进行第二次创建，将会失败，并出现冲突错误如下：
>docker: Error response from daemon: Conflict. The container name "/webid" is already in use by container "1f405a5b8b496ccaca2425924585d2c41fb9646ac886e490a96cf885dbcf83c0". You have to remove (or rename) that container to be able to reuse that name.
See 'docker run --help'. 

默认情况下，Docker给配一个为一的名字给他创建的每个容器。`--name`只是重写了该已知值的进程。如果出现以上冲突可以通过修改名字进行，
```sh
docker rename webid webid-old
```
通过`docker ps`查看第一个运行的名字是否改成功
重命名可以减轻一次命名冲突，但无法避免首要问题。除了名字，Docker分配一个唯一的标识符，是一个十六进制编码的1024位数字，如`1f405a5b8b496ccaca2425924585d2c41fb9646ac886e490a96cf885dbcf83c0`
，我们也可以通过该ID执行 `stop | exec` 命令。

一般docker生成的ID基本是唯一的，产生冲突几乎不可能，所以大多数Docker界面上你可以看到被截断成12个字符，在获取容器，可以使用他们
```sh
docker exec <12位字符> ps
docker stop <12位字符> 
```
获取容器ID的方式
    - 第一种：简单的启动或创建一个新容器，将命令的结果赋值给一个Shell变量。
    - 第二种：如果只想在创建容器使得到容器ID，交互式容器是无法做到的。可以用`docker create`命令。它和`docker run`命令类似，主要区别在于该容器是被停止状态创建的。
    