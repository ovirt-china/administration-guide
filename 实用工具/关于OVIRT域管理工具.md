# 关于OVIRT域管理工具

OVIRT虚拟化环境使用目录服务对用户进行管理和验证。要在OVIRT虚拟化环境中添加用户，首先通过admin@internal用户为MANAGER配置目录服务。添加、删除目录服务时使用*engine-manage-domains*命令。

只有OVIRTMANAGER服务器上安装了*engine-manage-domains*命令才可使用该命令。该命令必须由*root*用户执行。
