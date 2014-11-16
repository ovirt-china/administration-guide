# 准备 iSCSI 存储

为了添加 iSCSI 存储域，我们必须在 iSCSI 服务器上导出 iSCSI 服务。

安装相关软件包。

    # yum install -y scsi-target-utils


编辑 `/etc/tgt/targets.conf`
文件，增加以下几行内容（根据你的实际情况调整）：


    <target iqn.2014-03.com.example:server.target0>
        backing-store /dev/sdb # LUN 1
        backing-store /dev/sdc # LUN 2
    </target>



Target
通常由创建的年份以及月份，服务器所在的完全合格域名，服务器名称以及目标编号组成。

重启 tgtd 服务。

    # service tgtd restart


让 tgtd 服务开机启动。

    # chkconfig tgtd on


如果配置了 iptables 防火墙，必须把 iSCSI 用来和客户端通信的端口（默认是
3260）打开:

    # iptables -I INPUT 6 -p tcp --dport 3260 -j ACCEPT


保存 iptables 的配置。

    # service iptables save


*结果*.
现在，你已经创建好了一个 iSCSI 存储了，接下来就是把它添加到 OVIRT
管理系统中了。
