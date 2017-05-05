# VaneQ 部署

## 获取安装镜像

## VMWare 部署

### 部署 OVA 镜像

通过 `vsphere client` 登录到 `vcenter/esxi` 上，通过 `Deploy OVF Template|部署 OVF 模板` 并选择提供的镜像来部署

默认配置为 `4 core/6GB ram/40GB disk`, 建议修改内存为 `16GB`，并重启

![vmware-deploy](http://web-1253505474.cossh.myqcloud.com/docs/vmware-deploy.gif)

## OpenStack 部署

### 上传镜像到 Glance

```shell
$ glance image-create --disk-format qcow2 --container bare --is-public True --progress --name VaneQ --file darga-vaneq-latest.qcow2
```

### 通过镜像部署

```shell
$ nova boot --flavor ${your_flavor_name}-key-name ${your_key_namea} --image ${your_image_name} --nic net-id=${your_net_id} ${your_vm_name}
```

![openstack-cli-deploy](http://web-1253505474.cossh.myqcloud.com/docs/oepnstack-cli-deploy.gif)

### Web 页面部署

![openstack-web-deploy](http://web-1253505474.cossh.myqcloud.com/docs/openstack-web-deploy.gif)

## 初始化

登录 `vaneq` 主机 并通过 `vqctl config` 命令初始化

```shell
$ ssh vqctl@${vaneq_host} # 密码为 vqctl

# 如果是通过 vmware 部署，并没有 dhcp 的情况下
# 先通过 console 登录 vqctl 用户
# 再使用 vqctl config static_ip 命令 配置静态 IP 地址

$ vqctl config all

Seed Widgets? [y/N] # 建议启用, 初始化 dashboard 报表
Seed Service Catalogs? [y/N] # 初始化 服务目录项
Seed Application Deployment Catalog? [y/N] # 初始化 应用部署服务
Seed VMware Catalog? [y/N] # 初始化 VMWare 服务，必须先添加 VMWare 提供商
Seed OpenStack Catalog? [y/N] # 初始化 OpenStack 服务，必须先添加 OpenStack 提供商
Seed Init User and Projects? [y/N] # 建议启用, 初始化用户和项目
Open Captrue Utilization? [y/N] # 建议启用 较消耗资源, 开启虚拟机监控
Change Company Name? [y/N] # 修改公司名称
Config Static IP? [y/N] # 配置静态 IP
# Input You IP Address: 192.168.10.16
# Input You Prefix: 24
# Input You Gateway: 192.168.10.1
Build VaneQ Frontend? [y/N] # 首次配置必须启用, 构建前端项目
Restart Network? [y/N] # 配置完静态 IP 后必须重启，重启网络
Restart VaneQ Service? [y/N] # 建议配置完毕后重启, 重启 VaneQ 服务
```

通过 `vqctl status` 命令查看 `vaneq` 服务状态

```shell
vaneq -> vqctl status
● vaneqserverd.service - vaneq server daemon
   Loaded: loaded (/usr/lib/systemd/system/vaneqserverd.service; enabled; vendor preset: disabled)
   Active: active (running) since Fri 2017-04-28 11:51:49 CST; 3 days ago
  Process: 4739 ExecStop=/bin/sh -c /bin/vaneqserver.sh stop (code=exited, status=0/SUCCESS)
  Process: 4827 ExecStart=/bin/sh -c /bin/vaneqserver.sh start (code=exited, status=0/SUCCESS)
 Main PID: 4846 (ruby)
   CGroup: /system.slice/vaneqserverd.service
           ├─ 4846 VaneQ Server
           ├─ 5106 VaneQ: Vmware::InfraManager::MetricsCollectorWorker id: 180, queue: vmware
           ├─ 5118 VaneQ: Vmware::InfraManager::MetricsCollectorWorker id: 181, queue: vmware
           ├─ 5177 VaneQ: VaneQEmsMetricsProcessorWorker id: 186, queue: ems_metrics_processor
           ├─ 5187 VaneQ: VaneQEmsMetricsProcessorWorker id: 187, queue: ems_metrics_processor
           ├─ 5203 VaneQ: VaneQEmsRefreshCoreWorker id: 188, queue: ems_29
           ├─ 5279 VaneQ: Vmware::InfraManager::EventCatcher id: 192, queue: ems_29
           ├─ 5291 VaneQ: VaneQEventHandler id: 193, queue: ems
           ├─ 5338 VaneQ: VaneQPriorityWorker id: 196, queue: generic
           ├─ 5354 VaneQ: VaneQPriorityWorker id: 197, queue: generic
           ├─ 5369 VaneQ: VaneQReportingWorker id: 198, queue: reporting
           ├─ 5377 VaneQ: VaneQReportingWorker id: 199, queue: reporting
           ├─ 5390 VaneQ: VaneQScheduleWorker id: 200
           ├─ 5434 VaneQ: VaneQStorageMetricsCollectorWorker id: 203, queue: storage_metrics_collector
           ├─ 5457 puma 3.3.0 (tcp://0.0.0.0:5000) [VaneQ: Web Server Worker]
           ├─ 5478 puma 3.3.0 (tcp://0.0.0.0:3000) [VaneQ: Web Server Worker]
           ├─ 5494 VaneQ: VaneQVimBrokerWorker id: 206
           ├─ 5506 puma: cluster worker 0: 5457 [VaneQ: Web Server Worker]
           ├─ 5520 puma: cluster worker 1: 5457 [VaneQ: Web Server Worker]
           ├─ 5542 puma: cluster worker 0: 5478 [VaneQ: Web Server Worker]
           ├─ 5556 puma: cluster worker 1: 5478 [VaneQ: Web Server Worker]
           ├─ 5572 puma 3.3.0 (tcp://0.0.0.0:4000) [VaneQ: Web Server Worker]
           ├─ 5618 puma: cluster worker 0: 5572 [VaneQ: Web Server Worker]
           ├─ 5621 puma: cluster worker 1: 5572 [VaneQ: Web Server Worker]
           ├─13632 VaneQ: VaneQGenericWorker id: 218, queue: generic
           ├─18931 VaneQ: Vmware::InfraManager::RefreshWorker id: 331, queue: ems_29
           ├─18940 VaneQ: VaneQSmartProxyWorker id: 332, queue: smartproxy
           ├─18948 VaneQ: VaneQSmartProxyWorker id: 333, queue: smartproxy
           └─20073 VaneQ: VaneQGenericWorker id: 219, queue: generic
```

## 访问测试

启动后 通过浏览器访问 `${vaneq_host}:9000`

默认管理员账号密码为 `admin/smartvm`

如果初始化了用户和项目，会生成以下用户

- `user1/user1`
- `user2/user2`
- `itadmin/itadmin`
- `projectadmin/projectadmin`

## 排错

### 403 Forbidden

访问出现 `403` 错误，一般是因为 `vaneq` 前端构建有问题，可以通过 `vqctl config build_frontend` 重新构建

### API接口异常，请联系系统管理员

访问/登录 出现 `API接口异常，请联系系统管理员` 错误，登录 `${vaneq_host}` 通过 `vqctl status` 命令查看服务状态，一般是因为 `vaneq` 服务没有完全启动导致
