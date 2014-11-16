# OVIRT域管理工具的命令行说明

命令的使用方法如下：

    engine-manage-domains -action=ACTION [options]


可用的操作（ACTION）有：

add
为OVIRTMANAGER添加目录服务。

edit
编辑OVIRTMANAGER中的目录服务。

delete
为OVIRTMANAGER删除目录服务。

validate
验证OVIRTMANAGER中的目录服务。该操作会使用之前配置的用户和密码对所有目录服务进行验证尝试。

list
列出OVIRTMANAGER中的目录服务。

以下的命令行选项可以配合具体的操作一同使用：

-domain=DOMAIN
指定要进行操作的域。对于
*add*、*edit*和*delete*操作-domain是必须指定的。

-provider=PROVIDER
指定目录服务的类型，支持的目录服务有：

-   *ActiveDirectory* - Active Directory

-   *IPA* - Identity Management（IdM）

-   *RHDS* - Red Hat Directory
    Service。RHDS不使用Kerberos，而OVIRT虚拟化环境要求使用Kerberos，因此使用RHDS时需要配置Kerberos域中的一个目录服务。

    > **Note**
    >
    > 使用RHDS时必须安装*memberof*插件，使用*memeberof*插件要求用户都是*inetuser*用户。

-user=USER
指定目录服务的用户。在*add*操作中*-user*选项是必需的，*edit*操作则可以不会指定。

-passwordFile=FILE
指定密码文件，目录服务用户的密码在该文件的第一行。执行*add*操作时，*-passwordFile*或者*-interactive*选项必须使用其中一个。

-addPermissions
为指定的域用户赋予在OVIRTMANAGER中的*SuperUser*角色。默认的情况下，没有启用这一选项，指定的域用户不会获得*SuperUser*的角色。在*add*和*edit*操作中可以选择使用*-addPermissions*选项。

-interactive
指定域用户的密码是否手动（交互式）地提供。在*add*操作中，该选项和*-passwordFile*必须选择其中一个使用。

-configFile=FILE
指定命令配置文件的路径。不使用默认配置文件时，使用该选项。

-report
该选项和*validate*操作一起使用时，会生成在验证过程发生的所有错误信息的报告。

*engine-manage-domains*使用方法的完整说明也可以通过下面的命令获取：

    # engine-manage-domains --help

