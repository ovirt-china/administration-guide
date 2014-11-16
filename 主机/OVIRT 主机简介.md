# OVIRT 主机简介

主机，也被称作宿主机，是供虚拟机在其之上运行的物理服务器。OVIRT
中的虚拟化是由 KVM(Kernel-based Virtual Machine) 这个可动态加载的 Linux
内核模块提供的。

KVM 能够同时支持多个虚拟机，虚拟机之上的系统可以是 Windows 或者
Linux。虚拟机在主机之中是以 Linux 进程和线程的存在形式运行着，并且由
OVIRT MANAGER进行远程管理。OVIRT 环境中存在一个或者多个主机。

OVIRT 支持使用两种方式来安装主机。您可以使用 OVIRT
主机安装光盘，或者在一台标准的 RHEL/CentOS
之上安装主机所需要的软件包，来完成主机的安装。

OVIRT 主机可以使用针对虚拟化环境提供优化策略的 *tuned*
来进行配置，从而提高主机性能。关于 *tuned* 的更多信息，请参考 RHEL
文档中的相关章节。

OVIRT 主机默认启用了安全相关的特性。SELinux(Security Enhanced
Linux，安全强化 Linux) 和 iptables
防火墙默认都是启用的，并且您能够进行全方位的配置。MANAGER能够在 OVIRT
主机添加到 OVIRT 环境时打开所需要的端口。关于端口的详细列表，请参见?。

主机是一台带有 Intel VT 或者 AMD-V CPU 技术的 64
位服务器，在其之上运行着 RHEL/CentOS 6.1 及之后的 64 位版本操作系统。

在 OVIRT 平台上的物理主机，具备如下特点：

-   只能够属于系统中的一个集群。

-   其 CPU 必须支持 AMD-V 或者 Intel VT 硬件虚拟化扩展。

-   其 CPU 必须提供满足当创建集群时所选择的虚拟 CPU
    类型所需要的功能/指令集。

-   最少有 2 GB 内存。

-   能够使用系统权限为其分配一个系统管理员。

*参见：*

-   ?

-   ?

-   ?

-   ?

