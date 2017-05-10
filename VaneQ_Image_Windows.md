# VaneQ 镜像制作 (Windows)

## VMWare

制作 `Windows` 镜像需要安装 `vmware-tools` 和 `cloudbase-init`

下面是一个 `Windows 2008 R2` 安装的过程

### 创建虚拟机

创建虚拟机的过程可以看之前的文档 [创建虚拟机](/VaneQ_Image_Linux?id=创建虚拟机)

### 安装操作系统

!> 虚拟机系统类型 建议选择为 `Windows`

![windows-installation](http://web-1253505474.cossh.myqcloud.com/docs/windows-installation.gif)

### 安装 vmware-tools

!> 安装完后需要重启虚拟机

![windows-vmware-tool-installation](http://web-1253505474.cossh.myqcloud.com/docs/windows-vmware-tool-installation.gif)

### 安装 Cloudbase-init

下载 [Cloudbase-init](http://download.vanecloud.com/CloudbaseInitSetup_Stable_x64.msi)

![windows-cloudbase-init-installation](http://web-1253505474.cossh.myqcloud.com/docs/windows-cloudbase-init-installation.gif)

### 转换为模板

转换模板可以看之前的文档 [转换虚拟机为模板](/VaneQ_Image_Linux?id=%e8%bd%ac%e5%8c%96%e4%b8%ba%e6%a8%a1%e6%9d%bf)
