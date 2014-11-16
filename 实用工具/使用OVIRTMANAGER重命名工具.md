# 使用OVIRTMANAGER重命名工具

使用 *ovirt-engine-rename* 命令更新MANAGER的fqdn域名记录。

在DNS系统中准备好MANAGER新的fqdn域名记录以及其他相关记录。

如果使用DHCP，修改DHCP配置。

修改MANAGER服务器的主机名。

执行下面的命令：

    # /usr/share/ovirt-engine/setup/bin/ovirt-engine-rename


出现下面的提示时，按下*回车键*，关闭MANAGER：

    During execution engine service will be stopped (OK, Cancel) [OK]:

出现下面的提示时，输入新的fqdn域名：

    New fully qualified server name:[new name]

> **Note**
>
> *ovirt-engine-rename*
> 支持--name参数，参数后面直接指定MANAGER新的fqdn域名，可以省去后面提示输入域名的步骤，如：
>
>     # /usr/share/ovirt-engine/setup/bin/ovirt-engine-rename --name=[new name]
>

*ovirt-engine-rename* 会修改以下文件关联的MANAGER域名：

-   /etc/ovirt-engine/engine.conf.d/10-setup-protocols.conf

-   /etc/ovirt-engine/imageuploader.conf.d/10-engine-setup.conf

-   /etc/ovirt-engine/isouploader.conf.d/10-engine-setup.conf

-   /etc/ovirt-engine/logcollector.conf.d/10-engine-setup.conf

-   /etc/pki/ovirt-engine/cert.conf

-   /etc/pki/ovirt-engine/cert.template

-   /etc/pki/ovirt-engine/certs/apache.cer

-   /etc/pki/ovirt-engine/keys/apache.key.nopass

-   /etc/pki/ovirt-engine/keys/apache.p12

