- 配置docker环境
    - CentOS7  内核3.1以上版本 `uname -r`
    - 移除旧版本
    ```sh
    yum remove docker docker-common docker-selinux docker-engine 
    yum remove docker-ce
    rm -rf /var/lib/docker
    ```
    - 安装依赖包
    ```
    yum install -y yum-utils device-mapper-persistent-data lvm2         
    
    #安装前可查看device-mapper-persistent-data和lvm2是否已经安装 
    rpm -qa|grep device-mapper-persistent-data
    rpm -qa|grep lvm2
    ```
    - 设置yum源
    ```
    yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
    ```
    - 跟新yum软件包索引
    ```
    yum makecache fast
    ```
    - 安装
    ```
    yum install docker-ce -y #安装指定版本docker-ce可使用以下命令查看
    yum list docker-ce.x86_64 --showduplicates | sort -r # 安装完成之后可以使用命令查看
    docker version
    ```