# 使用 sys-unconfig 封装 Linux 虚拟机为一个模板准备部署

*摘要*.
使用 sys-unconfig
对虚拟机进行封装。这样可以避免多个基于该模板的虚拟机造成的冲突，例如 MAC
地址冲突等等。

登录该虚拟机。

删除 ssh host keys：

    # rm -rf /etc/ssh/ssh_host_*


在文件 `/etc/sysconfig/network` 中设置
*HOSTNAME=localhost.localdomain*。

在文件 `/etc/sysconfig/network-scripts/ifcfg-eth*` 中，删除 *HWADDR=*
所在一行。

删除所有位于 `/var/log` 下的日志和位于 `/root`
下的安装日志，此步骤不是必须的。

运行以下命令:

    # sys-unconfig


*结果*.
虚拟机将会关闭，此时虚拟机已经封装好了，可以基于此虚拟机制作模板了。用户可以基于创建的模板部署虚拟机而不用担心配置文件冲突的问题。
