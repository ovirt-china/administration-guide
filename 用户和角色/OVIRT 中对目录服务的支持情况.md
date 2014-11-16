# OVIRT 中对目录服务的支持情况

在安装过程中，OVIRT MANAGER创建其自己内部的管理员用户
*admin*。这个账户是为了初始化配置环境以及排解疑难问题而设计的。要添加用户到
OVIRT 环境中，您需要使用 OVIRT 的域管理工具 *engine-manage-domains*
来连接一个目录服务器到MANAGER

一旦至少一个目录服务器连接至MANAGER，您就可以使用管理员门户来添加该目录服务器中已存在的用户并为他们指派角色。用户以格式为
*user@domain* 的用户主体名称（User Principal
Name，UPN）来区分。连接多个目录服务器到MANAGER同样被支持。

OVIRT 支持如下的目录服务器：

-   Active Directory

-   Identity Management(IdM)

-   Red Hat Directory Server 9 (RHDS 9)

-   OpenLDAP

您还必须确保您的目录服务器有正确的 DNS
记录，尤其是必须确保有以下几条关于您的目录服务器的 DNS 记录：

-   一个有效的目录服务器的反向地址查找指标记录（PTR）。

-   一个有效的在 TCP 389 端口上的 LDAP 服务定位器（SRV）。

-   一个有效的在 TCP 88 端口上的 Kerberos 服务定位器（SRV）。

-   一个有效的在 UDP 88 端口上的 Kerberos 服务定位器（SRV）。

如果以上记录在 DNS 中不存在，您将不能够使用 *engine-manage-domains*
来添加域至 OVIRT MANAGER中。

关于安装和配置支持的目录服务器的更多详细信息，请参考各厂商的文档：

-   Active Directory -
    [](http://technet.microsoft.com/en-us/windowsserver/dd448614)

-   Identity Management (IdM) -
    [](http://docs.redhat.com/docs/en-US/Red_Hat_Enterprise_Linux/6/html/Identity_Management_Guide/index.html)

-   Red Hat Directory Server (RHDS) -
    [](http://docs.redhat.com/docs/en-US/Red_Hat_Directory_Server/index.html)

-   OpenLDAP - [](http://www.openldap.org/doc/)

> **Important**
>
> 您必须明确地在目录服务器中创建一个新用户作为 OVIRT
> 虚拟化环境的管理用户。*不要*使用目录服务器的管理用户作为 OVIRT
> 虚拟化环境的管理用户。

> **Important**
>
> 同一台机器上无法同时安装 OVIRT MANAGER和 IdM(ipa-server)。IdM 与 OVIRT
> MANAGER所依赖的 mod\_ssl 包不兼容。

> **Important**
>
> 如果您使用 Active Directory
> 作为目录服务器，并且您希望在创建模板和虚拟机的过程中使用
> *sysprep*，OVIRT 管理员用户必须被授权对域进行的操作包括：
>
> -   将一台计算机加入域
>
> -   修改域中组的成员
>
> 关于在 Active Directory
> 中创建用户账户的信息，请参考[](http://technet.microsoft.com/en-us/library/cc732336.aspx)。
>
> 关于在 Active Directory
> 中进行操作授权，请参考[](http://technet.microsoft.com/en-us/library/cc732524.aspx)。

> **Note**
>
> OVIRT MANAGER 使用 Kerberos 来与目录服务器进行认证。RHDS
> 并不提供原生的 Kerberos 支持。如果您使用 RHDS
> 作为目录服务器则您必须确保该目录服务器是作为一个有效的 Kerberos
> 域中的服务存在。要实现这个目标，您必须在参考相关的目录服务器文档的同时进行如下操作：
>
> -   为 RHDS 配置 *memberOf* 插件以允许组成员。尤其是要注意确保
>     *memberOf* 插件中的 *memberofgroupattr* 属性的值应该设置为
>     *uniqueMember*。在 *OpenLDAP* 中，*memberOf*
>     功能不被称作“插件”，而被称作“overlay”，并且不要求安装后进行任何配置。
>
>     参考 RHDS 9.0 插件指南获得关于更多配置 *memberOf* 插件的信息。
>
> -   在 Kerberos 域中将目录服务器以格式 *ldap/hostname@REALMNAME*
>     定义为服务。将 *hostname* 替换为目录服务器的完全合格域名，将
>     *REALMNAME* 替换为 Kerberos realm 的完全合格域名。Kerberos 的
>     realm 名称必须全部大写。
>
> -   在 Kerberos 域中为目录服务器生成一个 `keytab` 文件。该 `keytab`
>     文件包含 Kerberos 的 principal 与其对应的加密的 key 对。这些 key
>     将允许目录服务向 Kerberos 域认证其本身，
>
>     参考您的 Kerberos 的文档获得更多关于如何生成 `keytab` 文件的信息。
>
> -   将 `keytab` 文件安装到目录服务器。然后配置 RHDS 使其识别该
>     `keytab` 文件并接受使用 GSSAPI 的 Kerberos 认证。
>
>     参考 RHDS 9.0 系统管理员手册获得更多关于配置 RHDS 使用外部的
>     `keytab` 文件的信息。
>
> -   通过在目录服务器上使用 `kinit` 命令认证一个在 Kerberos
>     域中定义的用户来对配置进行测试。一旦认证成功，则对目录服务器执行
>     `ldapsearch` 命令。使用 *-Y GSSAPI* 确保使用 Kerberos 进行认证。
>
