---
layout: post
title: "Install OpenGauss"
date: 2023-12-24 23:19:00 +0800
categories: 
header-img: "img/post-bg.jpg"
header-mask: 0.3
---

## 安装OpenGauss

记录安装OpenGauss过程

### 安装依赖

```(bash)
yum install -y libaio-devel
yum install -y flex
yum install -y bison
yum install -y ncurses-devel
yum install -y glibc-devel
yum install -y patch
yum install -y readline-devel
yum install -y libnsl
# yum install -y redhat-lsb-core
yum install -y vim
```

redhat-lsb-core在OpenEuler找不到

### 关闭操作系统防火墙

修改/etc/selinux/config文件中的“SELINUX”值为“disabled”。

a. 使用VIM打开config文件

```(bash)
vim /etc/selinux/config
```

b. 修改“SELINUX”的值“disabled”，执行**:wq**保存并退出修改。

```(bash)
SELINUX=disabled
```

重新启动操作系统

c. 检查防火墙是否关闭。

```bash
systemctl status firewalld
```

若防火墙状态显示为active (running)，需要关闭防火墙

![2023-12-24-install-OpenGauss-20231224235742](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-OpenGauss-20231224235742.png)

d. 关闭防火墙

```bash
systemctl disable firewalld.service
systemctl stop firewalld.service
```

![2023-12-24-install-OpenGauss-20231224235826](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-OpenGauss-20231224235826.png)

### 设置字符集参数

在/etc/profile文件中添加`export LANG=en_US.UTF-8`（en_US.UTF-8可以换成其他Unicode编码）

```bash
vim /etc/profile
```

### 设置时区和时间

```bash
cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```

### 关闭swap交换内存（可选）

```bash
swapoff -a
```

### 关闭RemoveIPC

删除

```bash
sed -i '/^RemoveIPC/d' /etc/systemd/logind.conf
sed -i '/^RemoveIPC/d' /usr/lib/systemd/system/systemd-logind.service
```

新增
```bash
echo "RemoveIPC=no"  >> /etc/systemd/logind.conf
echo "RemoveIPC=no"  >> /usr/lib/systemd/system/systemd-logind.service
```

重新加载配置参数

```bash
systemctl daemon-reload
systemctl restart systemd-logind
```

检查修改是否生效

```bahs
loginctl show-session | grep RemoveIPC
systemctl show systemd-logind | grep RemoveIPC
```

![2023-12-24-install-OpenGauss-20231226000949](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-OpenGauss-20231226000949.png)

### 关闭HISTORY记录

为避免指令历史记录安全隐患，需关闭各主机的history指令。

修改根目录下/etc/profile文件。

```bash
vim /etc/profile
```

设置HISTSIZE值为0。例如，系统中HISTSIZE默认值为1000，将其修改为0。

```bash
HISTSIZE=0
```

保存/etc/profile。

```bash
wq
```

设置/etc/profile生效。

```bash
source /etc/profile
```

### 创建用户和目录

创建普通用户`omm`和目录，并授权

```bash
groupadd -g 1001 dbgrp
useradd -u 2001 -g dbgrp omm
mkdir -p /opt/software/openGauss
chown -R omm:dbgrp /opt
```

设置`oom`密码

```bash
passwd omm
```

切换到用户`omm`

```pash
su omm
```

### 下载软件包

在[官网](https://opengauss.org/zh/download/)获取极简版的下载连接

![2023-12-24-install-OpenGauss-20240107115059](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-OpenGauss-20240107115059.png)

下载到`/opt/software/openGauss`，`https://opengauss.obs.cn-south-1.myhuaweicloud.com/5.0.1/x86_openEuler_2203/openGauss-5.0.1-openEuler-64bit.tar.bz2`替换成官方获取到的路径

```bash
cd /opt/software/openGauss
wget https://opengauss.obs.cn-south-1.myhuaweicloud.com/5.0.1/x86_openEuler_2203/openGauss-5.0.1-openEuler-64bit.tar.bz2
```

### 安装软件包

解压刚才下载的压缩包`openGauss-5.0.1-openEuler-64bit.tar.bz2`（替换成你下载文件的名字）

```bash
tar -jxf openGauss-5.0.1-openEuler-64bit.tar.bz2 -C /opt/software/openGauss
```

如果报`tar: command not found`，安装`tar`

```bash
yum install -y tar
```

进入解压后目录下的simpleInstall

```bash
cd /opt/software/openGauss/simpleInstall
```

执行install.sh脚本安装openGauss

-w：初始化数据库密码

```bash
sh install.sh  -w "xxxx" &&source ~/.bashrc
```

如果安装显示报错`bash: ulimit: open files: cannot modify limit: Operation not permitted` 可以不用管或者执行

```bash
vim /etc/security/limits.conf
```

在配置文件中增加以下文本
```bash
gaussuser soft nofile 1000001
gaussuser hard nofile 1000002
```

安装执行完成后，使用ps和gs_ctl查看进程是否正常

```bash
ps ux | grep gaussdb
gs_ctl query -D /opt/software/openGauss/data/single_node
```

![2023-12-24-install-OpenGauss-``````](https://raw.githubusercontent.com/LoststarsJL/MyImage/main/markdown-image/2023-12-24-install-OpenGauss-%60%60%60%60%60%60.png)

### 重启服务器后如何启动服务

```bash
gs_ctl start -D /opt/software/openGauss/data/single_node -Z single_node
```