Docker提供用于监控和重启容器的几个选项：
- 自动重启容器

  使用`--restart`选项来自动重启容器
  ```
  docker run -d --name backoff-datector --restart always busybox date
  ```
  Docker并不总是立即重新启动容器，Docker采用了指数回退侧罗定时阐释重新启动，回退策略决定了连续尝试重新启动所需的时间间隔。指数回退策略将会花费在前一次等待连续尝试时间的2倍。
  
- 使用init和supervisor进程维持容器的运行状态

  init或supervisor进程，用于启动和维护其他程序状态。
  容器中的supervisor进程用来保持容器始终运行，即使目标进程出现故障并重启。
  下面来创建容器使用supervisord来确保所有相关的进程持续运行
  ```sh
  docker run -d -p 80:80 --name lamp-test tutum/lamp
  ```
  使用docker top命令查看该容器有哪些进程正运行着
  ```sh
  docker top lamp-test
  ```
  你会看到supervisord运行在程序清单中。现在可以通过手动停止容器内的某一进程，来测试supervisord的重启功能。
  在容器内杀死进程，需要知道它在容器中的PID值。运行exec自命令来获取
  ```sh
  docker exec lamp-test ps
  ```
  通过指定PID通过kill命令杀死进程
  ```sh
  exec lamp-test kill <PID>
  选择apache2的PID进行替换杀死
  ```
  当apache2停止时，supervisord进程会记录该事件，并重启该进程。
  通过`docker logs lamp-test`来查看日志
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  