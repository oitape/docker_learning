- 运行NGINX
```sh
docker run --detach --name web nginx:latest
```
> 运行此命令，Docker将从Docker Hub上的NGINX仓库下载、安装、运行该镜像软件，运行结束还有一串类似这样的数字
```
785e0931595766c33ee34e393fdb15955371c60072c218b5b131232487bc1282
```
这是运行NGINX容器的唯一标识符，标识符显示出来后，并不会发生什么，因为使用了--detach选项，并在后台启动该程序

静默运行在在后台的程序被称作守护程序，当你要在后台运行容器的守护程序，记得使用```--detach```标志或者它的缩写形式```-d```

- 运行邮件程序
```sh
docker run -d --name mailer dockerinaction/ch2_mailer
```

- 运行交互式容器
 ```sh
docker run --interactive --tty \
    --link web:web \
    --name web_test \
    busybox:latest /bin/sh
```
> --interactive：告诉Docker保持标准输入流对容器开放，即使容器没有终端连接。
--tty：告诉Docker为容器分配一个虚拟终端，这将允许你发送信号给容器。

用交互式容器的命令创建一个容器，启动一个UNIX shell，命令被链接到运行NGINX的容器上。

- 启动监控器
```sh
docker run -it \
    --name agent \
    --link web:insideweb \
    --link mailer:insidemailer \
    dockerinaction/ch2_agent
```
会看到终端一直在打印 ```System up```
如果需要后台运行 添加```-d```选项即可，（注意：暂停agent时【command + c】时，要先执行```docker rm agent```，再次尝试后台运行agent，你会看到终端不会再有相关log信息）
可通过 ```docker logs -f agent```来实时输出信息。















































