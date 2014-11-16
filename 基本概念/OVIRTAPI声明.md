# OVIRTAPI声明

OVIRT系统抛出了一系列使用的接口，方便用户和整个系统交互。这些接口
是对图形化的用户接口的一个补充。有了这些接口，开发人员可以做一些更高级,
自动化的开发。目前为止，OVIRT 系统的各个组件抛出了大部分接口，并且
这些接口完全可读写，仅有少部分接口是只读或者还没有完全被支持。

完全支持读写权限的接口

以下接口完全具有读写权限，可以直接利用下列接口和系统中的组件交互

Representational State Transfer(REST) API
在 OVIRT 系统中，REST API 完全被支持，你可以使用该接口和系统中
的组件交互。

Software Development Kit(SDK)
SDK 在 OVIRT 中也是被完全支持的，它是由 ovirt-engine-sdk 软件包 提供的。

Command Line Shell
OVIRT 系统完全支持命令行接口，该接口由 vdsm-cli 和 ovirt-engine-cli
软件包提供。

VDSM Hooks
目前，OVIRT 系统支持对虚拟机创建 VDSM Hooks，然后通过该 Hooks
修改虚拟机的配置。但是对主机的 Hooks 还不支持。

只支持读权限的接口

以下接口只支持读权限和系统交互:

OVIRT Manager History Database
目前仅仅支持 OVIRT Manager History Database 的读权限，写权限是
不允许的。

Libvirt
通过命令行 virsh -r 只读连接到 Libvirt
是完全支持的。但是写支持还不支持。

不支持的接口

以下接口目前还不支持:

vdsClient 命令
暂不支持使用这个命令和系统交互

Hypervisor Console
目前暂不支持使用除了用户图形界面以外的工具访问 Hypervisor Console。

数据库
不支持直接访问和操纵系统的数据库。
