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
    - 配置镜像加速
        - 1.注册登录开通阿里云容器镜像服务 
        - 2.查看控制台，招到镜像加速器并复制自己的加速器地址 
        - 3.找到/etc/docker目录下的daemon.json文件，没有则直接vi daemon.json
    ```
    #填写自己的加速器地址 
    {
        "registry-mirrors": ["https://zfzbet67.mirror.aliyuncs.com"] 
    }
    ```
    - 通知systemd重载此配置文件
    ```
    systemctl daemon-reload
    ```
    - 启动docker服务
    ```
    systemctl restart docker
    ```
    
- 启动一个mysql
```
    docker pull mysql:5.7
    #创建三个要挂载的目录
    mkdir -p /my/mysql/conf
    mkdir -p /my/mysql/data
    mkdir -p /my/mysql/logs
    #复制文件 并修改字符
    docker cp mysql:/etc/mysql/mysql.conf.d/mysqld.cnf /my/mysql/conf/ 
    vi /my/mysql/conf/mysqld.conf
    character-set-server=utf8 #最终启动命令 
    
    docker run \
    --name mysql \
    -p 3306:3306 \
    -v /my/mysql/conf:/etc/mysql/mysql.conf.d/ \ 
    -v /my/mysql/data:/var/lib/mysql \
    -v /my/mysql/logs:/logs \
    -e MYSQL_ROOT_PASSWORD=root \ 
    -d mysql:5.7
```