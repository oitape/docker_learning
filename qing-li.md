Docker中的清理只需要掌握几个简单的命令
使用`docker ps`命令查看当前正在运行中的程序。
使用`docker ps -a`查看所有正在运行和停止运行的程序。
使用`docker rm <CID or CNAME>`来移除容器。（移除正在运行的容器之前需要先停止）
使用`docker stop <CID or CNAME>`来停止正在运行的容器，或者使用`docker 人 -f <CID or CNAME>`标志停止一个进程。区别：
    - 使用-f标志，Docker发送SIG_KILL信号，立即终止接收过程。
    - 视同docker stop，将发送SIG_HUG信号。SIG_HUG的收件人有时间进行最后的退出和清理任务。SIG_KILL没有这样的允许时间，并可能导致文件损坏。