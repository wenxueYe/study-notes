# VirtualBox&Vagrant

> VirtualBox是一款x86的虚拟化虚拟机软件，而Vagrant则是虚拟机软件的操作工具。
>
> 当在windows主机上安装了虚拟机，则windows成为主机，虚拟机被称为是客户机。

[TOC]

<hr />

### 过程

#### VirtualBox

1. 开启计算机的CPU虚拟化
2. 下载和安装  [VirtualBox官网](https://www.virtualbox.org/)
3. 启动

#### Vagrant

1. 下载
    - [Vagrant官网](https://www.vagrantup.com/)
2. 寻找镜像 
    - [Vagrant镜像库](https://app.vagrantup.com/boxes/search)
3. 测试 
    - vagrant --version
4. 初始化Vagrant环境
    - vagrant init centos/7
5. 在Vagrant环境下操作虚拟机
    1. 启动虚拟机
        - vagrant up
    2. 连接虚拟机
        - vagrant ssh
    3. 切换至root用户
        - 初始密码为 vagrant
        - su root
    4. 重启虚拟机
        - vagarant reload

#### 备注

- 默认虚拟机即客户机的ip地址不是固定的ip，开发不方便，修改ip并且让主机和客户机能够ping通

    - Vagrantfile文件为客户机的环境配置

    - 过程

        - 主机命令：config

            - 查询主机以太网适配器 VirtualBox Host-Only Network

            - > 以太网适配器 VirtualBox Host-Only Network:
                >
                >    连接特定的 DNS 后缀 . . . . . . . :
                >    本地链接 IPv6 地址. . . . . . . . : fe80::64a7:3412:91f0:e52e%10
                >    IPv4 地址 . . . . . . . . . . . . : 192.168.56.1
                >    子网掩码  . . . . . . . . . . . . : 255.255.255.0
                >    默认网关. . . . . . . . . . . . . :

        - 修改vagrantfile内容，ip修改只需要保证24位相同，最后的主机号保持不一致即可

            ```shell
            config.vm.network "private_network", ip: "192.168.56.9"
            ```

        - 重启虚拟机并且查看客户机的ip地址

            - vagrant reload
            - ip addr

        - 互相ping测试

            - 主机向客户机

                - ping 192.168.56.9

            - 客户机向主机

                - ipconfig

                    > 无线局域网适配器 WLAN:
                    >
                    >    连接特定的 DNS 后缀 . . . . . . . :
                    >    IPv6 地址 . . . . . . . . . . . . : 2409:8910:1000:2f:32:54cd:f687:8e04
                    >    临时 IPv6 地址. . . . . . . . . . : 2409:8910:1000:2f:c086:bd11:dcaa:3adb
                    >    本地链接 IPv6 地址. . . . . . . . : fe80::32:54cd:f687:8e04%6
                    >    IPv4 地址 . . . . . . . . . . . . : 192.168.239.165
                    >    子网掩码  . . . . . . . . . . . . : 255.255.255.0
                    >    默认网关. . . . . . . . . . . . . : fe80::d4ff:eaff:fe88:b09d%6
                    >                                        192.168.239.240

                - ping 192.168.239.165

### [命令](https://www.vagrantup.com/docs/cli)

- 命令请在Vagrant环境执行

| 常用命令                                       | 功能                                                         | 备注 |
| ---------------------------------------------- | ------------------------------------------------------------ | ---- |
| vagrant --version                              | 查看版本号                                                   |      |
| vagrant init [name [url]]                      | 通过创造一个初始化的Vagrantfile文件初始化当前目录为一个Vagrant环境 |      |
| vagrant ssh                                    | 这将通过 SSH 连接到正在运行的 Vagrant 机器并让您访问 shell。 |      |
| vagrant up                                     | 启动虚拟机                                                   |      |
| vagrant reload                                 | 重启虚拟机                                                   |      |
| vagrant upload source [destination] [name\|id] | 此命令将文件和目录从主机上传到客户机。                       |      |

