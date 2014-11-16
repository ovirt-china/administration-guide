# 关于OVIRTMANAGER重命名工具

在初始环境下运行 *engine-setup*
命令，会根据安装过程中提供的fqdn域名生成一系列证书和密钥。如果后期需要修改MANAGER的fqdn域名（例如，将MANAGER迁移到另一个网络环境），需要使用
*ovirt-engine-rename* 命令完成所有相关的调整。
