# Docker&MySQL、Redis的安装

> 在客户机上安装docker，并且下载镜像，装配容器。
>
> [docker镜像库](https://hub.docker.com/)
>
> [docker文档](https://docs.docker.com/)

[TOC]

<hr />

### 过程

#### docker

1. [Centos系统上安装docker教程](https://docs.docker.com/engine/install/centos/)

    1. 卸载旧版本

        ```shell
         sudo yum remove docker \
                          docker-client \
                          docker-client-latest \
                          docker-common \
                          docker-latest \
                          docker-latest-logrotate \
                          docker-logrotate \
                          docker-engine
        ```

    2. 安装`yum-utils`包（提供`yum-config-manager` 实用程序）并设置**稳定的**存储库。

        ```shell
         sudo yum install -y yum-utils
         
         sudo yum-config-manager \
            --add-repo \
            https://download.docker.com/linux/centos/docker-ce.repo
        ```

    3. 安装*最新版本*的 Docker Engine 和 containerd

        ```shell
         sudo yum install docker-ce docker-ce-cli containerd.io
        ```

    4. 启动 Docker

        ```shell
         sudo systemctl start docker
        ```

    5. 通过运行`hello-world` 镜像来验证 Docker 引擎是否已正确安装。

        - 此命令下载测试映像并在容器中运行它。当容器运行时，它会打印一条消息并退出。

            ```shell
             sudo docker run hello-world
            ```

2. 设置Docker自启动

    - 不用每次启动客户机就手动开启docker

    ```shell
    sudo systemctl enable docker
    ```

3. 配置docker阿里云镜像加速

    - 位置

        - 阿里云官网-登录--控制台--左侧菜单--产品与服务--容器镜像服务--镜像加速器--Centos

    - ```shell
        sudo mkdir -p /etc/docker
        
        sudo tee /etc/docker/daemon.json <<-'EOF'
        {
          "registry-mirrors": ["https://5zdffhp9.mirror.aliyuncs.com"]
        }
        EOF
        
        sudo systemctl daemon-reload
        
        sudo systemctl restart docker
        ```

#### MySQL

1. 从镜像库拉取镜像

    ```shell
    sudo docker pull mysql:5.7
    ```

2. 查看镜像

    ```shell
    sudo docker images
    ```

3. 创建实例并启动

    ```shell
    docker run -p 3306:3306 --name mysql \
    -v /mydata/mysql/log:/var/log/mysql \
    -v /mydata/mysql/data:/var/lib/mysql \
    -v /mydata/mysql/conf:/etc/mysql \
    -e MYSQL_ROOT_PASSWORD=root \
    -d mysql:5.7
    
    # 解释
    # 给待创建的容器起别名 --name mysql
    # -p 3306:3306 将容器的3306端口映射到虚拟机的3306端口
    # -v /mydata/mysql/log:/var/log/mysql 将日志文件挂载到主机
    # -v /mydata/mysql/data:/var/lib/mysql 将配置文件挂载到主机
    # -v /mydata/mysql/conf:/etc/mysql 将配置文件夹挂载到主机
    # -e MYSQL_ROOT_PASSWORD=root 初始化root用户的密码
    # -d mysql:5.7 就是以后台方式运行，以及指定启动的镜像
    # -v 都是目录挂载，就是说mysql的一切东西都是在容器内部中的相应目录下，为了方便修改，不用每次修改的时候进入容器内部，所以将容器的目录挂载（映射）到主机中，理解为快捷方式？
    ```

4. 查看正在运行中的容器

    ```shell
    sudo docker ps
    
    # 选项 -a查看所有容器（包括未启动）
    ```

5. 以交互模式进入容器

    ```shell
    sudo docker exec -it mysql /bin/bash
    ```

6. 测试连通

    ```shell
    mysql -u root -p root
    - IP：192.168.56.9
    - 账户&密码：root root
    ```

7. 退出容器

    ```shell
    exit
    # 容器可以被看做一个linux系统，所以用的也是linux的命令
    ```

8. <span style="color:red">修改MySQL的部分配置</span>

    ```shell
    # 暂时省略
    ```

9. 重启容器

    ```shell
    sudo docker restart mysql
    ```

#### Redis

1. 从镜像库拉取镜像

    ```shell
    sudo docker pull redis
    ```

2. 创建实例并启动

    ```shell
    # 容器中的/etc/redis.conf挂载到主机的时候，如果直接创建实例挂载的话，会因为redis.conf不存在而直接将redis.conf当成目录创建，所以避开这个坑，要先手动创建
    
    sudo mkdir -p /mydata/redis/conf
    sudo touch /mydata/redis/conf/redis.conf
    
    sudo docker run -p 6379:6379 --name redis \
    -v /mydata/redis/conf/redis.conf:/etc/redis/redis.conf \
    -d redis redis-server /etc/redis/redis.conf
    ```

3. 以交互模式执行redis-cli命令连接

    ```shell
    sudo docker exec -it redis redis-cli
    ```

4. redis持久化

    ```shell
    # 修改配置文件 /mydata/redis/conf/redis.conf
    # 持久化
    
    # 追加内容为：
    appendonly yes    
    
    # 再以交互模式执行redis-cli命令连接后测试持久化
    # redis配置文件见官网
    ```

5. 以可视化工具操作redis

    - Redis Desktop Manager

<hr />

### 命令

- 非正规，详情见官网

| 命令                                        | 功能                       | 备注                    |
| ------------------------------------------- | -------------------------- | ----------------------- |
| sudo systemctl start docker                 | 启动Docker                 |                         |
| sudo docker run hello-world                 | 测试Docker                 |                         |
| sudo docker images                          | 查看镜像                   |                         |
| sudo systemctrl enable docker               | 设置Docker自启动           |                         |
| sudo docker ps [-a]                         | 查看容器                   |                         |
| sudo systemctl daemon-reload                | 重新加载某个服务的配置文件 |                         |
| sudo systemctl restart docker               | 重新启动Docker             |                         |
| sudo docker pull ImageName:Tags             | 拉取镜像                   | Tags省略时下载最新      |
| sudo docker exec -it 容器ID或别名 /bin/bash | 以交互模式进入容器的控制台 |                         |
| sudo docker run [--name xxx -p xxx etc...]  | 创建容器实例并启动         |                         |
| exit                                        | 从容器中退出               | 因为容器和Linux系统相同 |
| etc...                                      |                            |                         |
