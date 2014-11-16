# OVIRT MANAGER防火墙要求

OVIRT
MANAGER要求系统防火墙开放一系列的端口以允许网络流量通过。`engine-setup`
脚本能够自动配置防火墙，但将会覆盖现有的防火墙配置。

当系统上已经有一些防火墙的配置时，为了避免这些配置被覆盖并失效，MANAGER所需要的防火墙规则必须被手动添加。`engine-setup`
命令在 `/usr/share/ovirt-engine/conf/iptables.default.in`
文件中保存了所需要的 *iptables* 规则列表。

文档中所示的防火墙配置以常见的默认端口配置为基础。如果安装过程中选择了非默认的
HTTP 和 HTTPS
端口，则您需要调整文档中所示的防火墙规则以允许网络流量通过您所选择的端口，而不是这里所列出的默认端口（*80*
和 *443*）。

|端口|协议|源机器|目标机器|目的|
|----|----|------|--------|----|
|-|ICMP|-   OVIRT NODE<br/><br/>|-   OVIRT MANAGER<br/><br/>|当注册到 OVIRT MANAGER时，OVIRT NODE发送一个 ICMP ping 请求至MANAGER以确认其在线。|
|22|TCP|-   用以维护MANAGER的系统，包括后台维护、配置和软件升级<br/><br/>|-   OVIRT MANAGER<br/><br/>|SSH（可选）|
|80、443|TCP|-   管理员门户客户端<br/><br/>-   用户门户客户端<br/><br/>-   OVIRT NODE<br/><br/>-   REST API 客户端<br/><br/>|-   OVIRT MANAGER<br/><br/>|提供到 MANAGER的 HTTP 和 HTTPS 连接。|

> **Important**
>
> 在 OVIRT MANAGER所在的机器需要导出 NFS 存储，例如 ISO
> 存储域的环境中，额外的端口必须被添加以允许 NFS
> 相关的网络流量通过防火墙。根据 NFS
> 版本的不同，需要在防火墙上打开如下端口：
>
> *NFSv4*
>
> -   TCP 端口 *2049*（NFS）
>
> *NFSv3*
>
> -   TCP 和 UDP 端口 *2049*（NFS）
>
> -   TCP 和 UDP 端口 *111*（*rpcbind*/*sunrpc*）
>
> -   使用 *MOUNTD\_PORT="port"* 指定的 TCP 和 UDP 端口
>
> -   使用 *STATD\_PORT="port"* 指定的 TCP 和 UDP 端口
>
> -   使用 *LOCKD\_TCPPORT="port"* 指定的 TCP 端口
>
> -   使用 *LOCKD\_UDPPORT="port"* 指定的 UDP 端口
>
> *MOUNTD\_PORT*、*STATD\_PORT*、*LOCKD\_TCPPORT*、*LOCKD\_UDPPORT*
> 等端口的配置在 `/etc/sysconfig/nfs` 文件中。

