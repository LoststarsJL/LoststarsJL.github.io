---
layout: post
title: "Install OpenEuler"
date: 2023-12-24 20:31:00 +0800
categories: 
header-img: "img/post-bg.jpg"
header-mask: 0.3
---

## 安装OpenEluer

记录安装OpenEluer过程

### 下载映像

1. 打开[官网](https://www.openeuler.org/zh/)
2. 下载映像

![2023-12-24-install-openEuler-20231224203703](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-openEuler-20231224203703.png)

### 新建虚拟机

1. 使用典型配置新建虚拟机

![2023-12-24-install-openEuler-20231224204518](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-openEuler-20231224204518.png)

2. 映像选择刚下载的映像

![2023-12-24-install-openEuler-20231224205348](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-openEuler-20231224205348.png)

3. 系统选择`Linux`，版本选择`其他 Linux 5.x`

![2023-12-24-install-openEuler-20231224205413](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-openEuler-20231224205413.png)

4. 选择安装路径

![2023-12-24-install-openEuler-20231224205543](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-openEuler-20231224205543.png)

5. 指定磁盘容量

![2023-12-24-install-openEuler-20231224205619](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-openEuler-20231224205619.png)

6. 修改内存和处理器核心数

![2023-12-24-install-openEuler-20231224205642](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-openEuler-20231224205642.png)

![2023-12-24-install-openEuler-20231224205711](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-openEuler-20231224205711.png)

![2023-12-24-install-openEuler-20231224205734](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-openEuler-20231224205734.png)

### 安装系统

1. 开启虚拟机

![2023-12-24-install-openEuler-20231224205804](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-openEuler-20231224205804.png)

2. 进入安装设置

![2023-12-24-install-openEuler-20231224210324](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-openEuler-20231224210324.png)

3. 设置磁盘，选择自动分区

![2023-12-24-install-openEuler-20231224210414](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-openEuler-20231224210414.png)

![2023-12-24-install-openEuler-20231224211034](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-openEuler-20231224211034.png)

4. 设置root账号

![2023-12-24-install-openEuler-20231224211419](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-openEuler-20231224211419.png)

5. 开始安装

![2023-12-24-install-openEuler-20231224211535](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-openEuler-20231224211535.png)

![2023-12-24-install-openEuler-20231224211759](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-openEuler-20231224211759.png)

![2023-12-24-install-openEuler-20231224211930](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-openEuler-20231224211930.png)

### 使用SSH连接虚拟机

#### 查看虚拟机ip

```(bash)
ifconfig
```

![2023-12-24-install-openEuler-20231224214946](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-openEuler-20231224214946.png)

如果显示command not found，需要安装ifconfig

![2023-12-24-install-openEuler-20231224214224](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-openEuler-20231224214224.png)

安装ifconfig

```(bash)
yum install -y net-tools
```

#### 安装openssh(可选)

安装openssh-client

```(bash)
sudo apt-get install openssh-client
```

安装openssh-server

```(bash)
sudo apt-get install openssh-server
```

启动ssh-server

```(bash)
sudo /etc/init.d/ssh restart
```

确认ssh-server工作正常

```(bash)
netstat -tpl
```

能看到ssh表示正常

#### 配置虚拟机防火墙

启用22端口并重启防火墙：

```(bash)
firewall-cmd --permanent --add-port=22/tcp
firewall-cmd --reload
```

#### 查看本机ip

```(bahs)
ipconfig
```

![2023-12-24-install-openEuler-20231224214821](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-openEuler-20231224214821.png)

#### 设置端口映射

编辑 -> 虚拟网络编辑器

![2023-12-24-install-openEuler-20231224215128](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-openEuler-20231224215128.png)

![2023-12-24-install-openEuler-20231224215211](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-openEuler-20231224215211.png)

ip地址用虚拟机的ip地址，主机端口号随意

![2023-12-24-install-openEuler-20231224220632](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-openEuler-20231224220632.png)

#### 使用mobaXterm连接

ip地址用宿主机的ip地址，端口号是刚才设置的端口号

![2023-12-24-install-openEuler-20231224220758](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-openEuler-20231224220758.png)

输入密码即可连接成功