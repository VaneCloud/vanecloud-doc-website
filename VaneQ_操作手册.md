# 产品简介

!> `vaneQ`氢氧云管平台是中科氢氧云计算技术（上海）有限公司结合多年的国内企业云计算平台建设经验和对于企业对于云计算平台管理需求的理解而打造的一款企业级混合云管理平台软件（Cloud Management Platform，简称CMP）。<br><br>
`vaneQ`运行在企业的云计算基础架构层（Infrastructure As a Service，简称IaaS）之上，向下对接企业传统IT资源和云资源池，向上为云管理员提供整体化的IT资源管理能力，为最终用户提供一条龙的的云服务交付。<br>
<br>
`vaneQ`通过对于 vaneCloud、OpenStack、Vmware、PowerVC等云计算基础架构平台管理的实现，配合整合企业常用IT服务的云服务化，扫清了企业使用云计算的"最后一公里"障碍，实现多数据中心、多资源池的异构混合云的统一管理。<br>
<br>
`vaneQ`可以协助企业实现全局的私有云管理，加速服务交付速度，提升效率和服务水平，最大化资源使用率。 通过`vaneQ`，企业可以从现有的虚拟化方式迁移到私有云或者混合云方式，以增强自身扩展云模式的能力，提升企业基础架构的灵活性。除此之外，通过自助服务、工作流审批、配额管理、容量评估和分析等自动化引擎，可以的优化客户原有工作方式，节约时间成本。

# 主要概念

## 项目

`vaneQ`中的项目借用了云计算概念中所谓的租户。租户包含在系统中可识别为指定用户的一切数据。也可以直接对应客户实际环境中的生产项目。

## 用户

用户是操作`vaneQ`的人员，可以直接对应到客户实际环境中的员工。

## 部门

部门是用户的集合。`vaneQ`中部门可以与客户实际组织架构做到一一对应。用户必然属于一个部门，但是一个用户可以拥有多个不同的项目，每个用户在不同项目中的角色也可以不同。

## 角色

角色是用来定义用户权限的概念。在`vaneQ`中默认定义了普通用户，IT管理员，项目管理员，超级管理员。在审批流程中，默认先由IT管理员审批，再由项目管理员审批。IT管理员和项目管理员默认只是角色不同，用来区分实际环境中的不同角色。超级管理员可以执行添加集群等更高级的操作。

## 集群

集群是接入`vaneQ`的基础架构云的接口定义。可以直接对应实际环境中的VMWare集群，或者OpenStack集群等。

## 服务

服务是定义了一系列既定流程的集合。`vaneQ`通过服务的形式规范了用户的操作，并通过自动化的方式实现既定的流程操作，例如新建云主机并安装软件等操作。

## 云主机

`vaneQ`中的云主机即是基础架构云中的云主机，或者虚拟机的概念。

# 操作手册

## 登陆云管平台

!> 默认端口:9000 默认管理账户：admin（管理账号） 默认密码：smartvm

![图1：云管登陆界面](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image3.png)

## 首页展示

![图2：云管登陆首页](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image4.png)

## 部门管理

!> 简要说明：部门管理主要包含对部门的 添加，修改，删除。部门管理的操作用户必须得是administrator用户

### 添加部门

操作步骤：权限控制组织架构添加添加部门

![图3：添加部门操作示意图](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image5.png)

### 修改部门名称

操作步骤：权限控制组织架构点击"你要修改的部门"编辑信息

![图4：部门修改操作示意图](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image6.png)

### 删除部门

!> 简要说明：删除部门时必须确定该部门下不存在任何项目，不然无法删除

![图5：删除部门](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image7.png)

## 项目管理

!> 简要说明：项目管理操作用户必须是administrator用户。主要包括 新建项目，项目配额管理，项目成员管理，修改项目名称，删除项目

### 添加项目

操作步骤: 权限控制组织架构添加添加项目

![图6：添加项目](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image8.png)

### 项目分配资源

您所管理的项目管理配额{CPU,内存,硬盘,虚拟机}总配额(输入配额)确定

![图7：项目配额管理](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image9.png)

![图8：项目配额配置完成后效果](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image10.png)

### 项目成员分配

!> 简要说明：默认有三个用户角色（IT管理员,项目管理员,普通用户）； 操作步骤: 编辑项目成员+图标；将用户添加到项目的相关用户角色中去；

![图8：项目成员分配](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image11.png)

![图8：项目成员分配后效果图](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image12.png)

### 删除项目

!> 操作说明：删除项目时，得确认该项目中无用户存在，有用户存在时是无法删除该项目的。

![图9：删除项目](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image13.png)

## 用户管理

!> 简要说明：用户管理操作主要有 添加用户，删除用户，修改用户名称，修改密码 操作用户administrator

### 新建用户

操作步骤：权限控制用户管理添加用户

![图10:添加用户](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image14.png)

权限设置中选择新建用户在某个项目中所扮演的角色（一个用户可以管理多个项目

![图11:添加用户界面展示](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image15.png)

### 修改用户名字

![图12：修改用户名](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image16.png)

### 删除用户

![图12：删除用户](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image17.png)

### 修改用户密码

![图13：修改用户密码](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image18.png)

## 群集管理

!> 群集管理：主要是添加群集和删除群集，操作用户administrator，群集指的是后台被管理计算节点，目前支持 VMware,openstack两种节点

![图14：群集管理主页（默认VMware)](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image19.png)

### 添加VMware群集

!> 简要说明：添加群集后云管会和后台进行资源同步所以需要等待一会儿

![图15：添加vmware群集](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image20.png)

![图16：添加vmware后验证](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image21.png)

### 添加openstack群集

![图17：添加openstack群集](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image22.png)

### 删除群集

![图18：删除群集](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image23.png)

## 云主机申请

!> 简要说明:云主机申请可以选择不同的计算节点类型，可以主机和所用的软件一起申请，也可以先申请云主机再装软件操作灵活

![图19：云主机申请界面](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image24.png)

### 云主机申请审批流程

!> 审批流程：普通用户 --> IT管理员 --> 项目管理员 非 Administrator 不可以自动审批

#### 用户申请主机

操作步骤：服务目录服务类别选择"虚拟机类型"

![图20：申请主机页面](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image26.png)

#### IT管理员审批

操作步骤：登陆 IT管理员我的请求申请中申请请求

![图21：审批流程展示](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image27.png)

#### 项目管理员审批

操作步骤：登陆 项目管理员我的请求申请中申请请求

![图22：审批流程展示](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image28.png)

#### 申请信息完成

![图23：审批完成](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image29.png)

#### 云主机创建完成验证

![图24：申请完成页面](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image30.png)

![图25：登陆nginx页面](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image31.png)

## 云主机操作

### 云主机操作

!> 简要说明：云主机开机，关机，挂起，console，删除等操作有两个入口分别是 '我的项目'和 '群集'当该用户有主机时才能执行上面的操作。

#### 我的项目

操作步骤：服务目录我的项目

![图26:我的项目操作入口](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image32.png)

![图27：主机列表及能执行的操作](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image33.png)

#### 计算群集 简要说明：计算群集中列出了该计算节点的所有主机，与1.8.1.1 我的项目不同（按用户）

![图28:列出计算节点所有虚拟机](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image34.png)

![图29：虚拟机操作属性](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image35.png)

### 云主机关机

![](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image36.png)

![图30：关闭云主机](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image37.png)

### 使用console 操作步骤：点击console按钮之后会页面会跳转到该主机的tty终端上

![图31：使用console管理](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image38.png)

![](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image39.png)

## 计费

![图32：计费界面](http://web-1253505474.cossh.myqcloud.com/docs/vaneq_manual/image40.png)
