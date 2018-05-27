# Keepalived for Kubernetes cluster setup
Keepalived for Kubernetes cluster setup

使用方法：

编辑start-keepalived.sh文件，修改虚拟IP地址VIRTUAL_IP、虚拟网卡设备名INTERFACE、虚拟网卡的子网掩码NETMASK_BIT、路由标识符RID、虚拟路由标识符VRID的值为实际Kubernetes集群所使用的值：

（CHECK_PORT的值6444一般不用修改，它是HAProxy的暴露端口，内部指向Kubernetes Master Server的6443端口）

例如：
```
#!/bin/bash
VIRTUAL_IP=192.168.9.30
INTERFACE=ens33
NETMASK_BIT=24
CHECK_PORT=6444
RID=10
VRID=160
```

运行start-haproxy.sh脚本
```
bash start-keepalived.sh
```

附注：为避免与局域网内其它使用Keepalived虚拟IP的应用产生冲突，请先用tcpdump抓包工具探测一下局域网内所使用的RID及VRID值，命令如下：

```
tcpdump -nn -i any net 224.0.0.0/8
```
