# VaneQ 镜像制作 (Linux)

## VMWare

和 `OpenStack` 镜像的制作过程差不多，但是必须安装 `vmware-tools`，使 `VCenter` 能够获取到虚拟机的 `IP`, 否则 `VaneQ` 应用部署功能则不能使用

下面是一个 `CentOS` 镜像制作的例子

### 创建虚拟机

通过 `ESXI/VCenter` 创建虚拟机，选择 `ISO` 文件进行安装

![centos-create](http://web-1253505474.cossh.myqcloud.com/docs/vmware-centos-create.gif)

### 安装操作系统

最小化安装即可

![centos-installation](http://web-1253505474.cossh.myqcloud.com/docs/centos-installation.gif)

### 初始化

#### 启用传统网卡命名方式

```shell
$ vi /etc/default/grub
... # 在 CMDLINE_LINUX 最后附加两个参数
GRUB_CMDLINE_LINUX='... net.ifnames=0 biosdevname=0'
...

$ grub2-mkconfig -o /boot/grub2/grub.cfg # 重新生成 grub 配置文件

$ systemctl disable NetworkManager # 关闭 NetworkManager

$ systemctl disable firewalld # 关闭 firwalld

$ ls /etc/sysconfig/network-scripts/ifcfg-*|grep -v ifcfg-lo|xargs rm -rf # 删除无关的 网卡配置
```

#### 安装 cloud-init

```shell
# 通过这种方式安装，需要互联网连接
$ yum install epel-release -y # 安装 epel 源

$ yum install cloud-init -y # 安装 cloud-init
```

#### 安装 vmware-tools

选择虚拟机 --> `Guest` --> `Install/Upgrade VMware Tools`

![vmware-tools](http://web-1253505474.cossh.myqcloud.com/docs/vmware-tools.png)

在终端中配置

```shell
$ yum install perl -y # 先安装 perl 语言

$ mount /dev/sr0 /mnt/ # 挂载 vmware-tools 到 /mnt
mount: /dev/sr0 is write-protected, mounting read-only

$ ls /mnt/
manifest.txt  run_upgrader.sh  VMwareTools-9.4.11-2400950.tar.gz  vmware-tools-upgrader-32  vmware-tools-upgrader-64

$ cp /mnt/VMwareTools-9.4.11-2400950.tar.gz .

$ tar xf VMwareTools-9.4.11-2400950.tar.gz

$ cd vmware-tools-distrib/

$ echo yes | ./vmware-install.pl # 全部 yes

open-vm-tools are available from the OS vendor and VMware recommends using
open-vm-tools. See http://kb.vmware.com/kb/2073803 for more information.
Do you still want to proceed with this legacy installer? [no]
Creating a new VMware Tools installer database using the tar4 format.

Installing VMware Tools.

... ignore ...

Enjoy,

--the VMware team
```

在 `VCenter` 中能够看到虚拟机的 `IP` 即可

![vmware-vm-ip](http://web-1253505474.cossh.myqcloud.com/docs/vmware-vm-ip.png)

#### 开启 CPU/内存 热插拔

不开启热插拔会导致 `vaneq` 自带的 `vmware` 虚拟机重新配置服务不可用

![vmware-vm-hot-plug](http://web-1253505474.cossh.myqcloud.com/docs/vmware-vm-hot-plug.png)

#### 转化为模板

![vmware-vm-to-template](http://web-1253505474.cossh.myqcloud.com/docs/vmware-vm-to-template.png)

## OpenStack

只需要标准的 `openstack` 镜像即可，可以参考 [OpenStack 官方手册](https://docs.openstack.org/image-guide/create-images-manually.html)
