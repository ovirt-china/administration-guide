# OVIRT 主机

OVIRT 主机是一个定制过的 Linux
系统，其上面只有运行虚拟机所需要的相关软件包。主机是无状态的，并且除非被明确要求，否则它将不会往硬盘上写入其它内容。

OVIRT 主机能够从 OVIRT
MANAGER中直接添加并且进行配置。另外您也可以在主机上进行配置使其主动连接到
OVIRT MANAGER；在MANAGER上只需要批准该台主机加入环境中即可。

与普通的 RHEL/CentOS 主机不同的是，OVIRT
主机无法作为一台存储节点被添加到启用了 Gluster 服务的集群中。

> **Important**
>
> OVIRT 主机是一个封闭的系统。如果您需要安装其它 rpm
> 软件包，请使用普通的 RHEL/CentOS 主机。

