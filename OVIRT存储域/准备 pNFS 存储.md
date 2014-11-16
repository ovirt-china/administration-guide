# 准备 pNFS 存储

作为对传统 NFS 的巨大改善，pNFS 一出世就得到了大家的认同。当使用 pNFS
协议的时候，客户端可以充分利用它的并行传输协议改善系统性能。pNFS
支持三种存储/布局模式：files，objects，blocks。但是请注意，目前 OVIRT
管理系统仅支持文件的存储模式。

为了验证 pNFS 能否在系统上使用，可以使用以下的挂载参数挂载一个 pNFS
的服务器:

    # -o minorversion=1


或者

    # -o v4.1


设置 pNFS 路径的权限以使得 OVIRT 能够进行访问：

    # chown 36:36 [pNFS 资源路径]


第一次挂载 pNFS，nfs\_layout\_nfsv41\_files
模块会自动的被加到到内核中，可以验证该模块是否被加载:

    # lsmod | grep nfs_layout_nfsv41_files


还可以使用 mount 命令验证是否成功使用 NFSv4.1 挂载。该命令的输出项使用
NFSv4.1 挂载的项目将会包含 minorverion=1 字样。
