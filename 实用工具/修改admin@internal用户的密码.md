# 修改admin@internal用户的密码

使用*root*用户登录到OVIRTMANAGER服务器。

使用*engine-config*命令为*admin@internal*设置新的密码：

    # engine-config -s AdminPassword=interactive


如果密码中有特殊字符，注意使用转义。

重启MANAGER使新的密码生效：

    # service ovirt-engine restart

