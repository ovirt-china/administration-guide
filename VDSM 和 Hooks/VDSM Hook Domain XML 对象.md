# VDSM Hook Domain XML 对象

Hook 脚本开始执行之后，*\_hook\_domxml*
变量将会被添加至运行环境中。该变量存放了表示对应的虚拟机的 libvirt
domain XML 文件的路径。下面列出的几个 Hook 是这个规则的例外。

对于以下列出的事件所触发执行的 Hook 脚本，*\_hook\_domxml*
变量存放的路径中的文件包含的是虚拟机网卡的 XML 表示而不是虚拟机的 XML
表示：

-   *\*\_nic\_hotplug\**

-   *\*\_nic\_hotunplug\**

-   *\*\_update\_device*

-   *\*\_device\_create*

-   *\*\_device\_destroy*

-   *\*\_device\_migrate\_\**

> **Important**
>
> *before\_migration\_destination* 和 *before\_vm\_dehibernate*
> 两个事件所触发执行的 Hook 脚本目前都是从源主机上获得 libvirt domain 的
> XML。在目标主机上的 XML 可能有一些不同之处。

VDSM 使用 libvirt domain XML 格式定义虚拟机。关于 libvirt domain XML
格式的详细信息能够从[](http://libvirt.org/formatdomain.html)中获得。虚拟机的
UUID 能够从 domain XML 中获得，也可以通过读取系统环境变量 *vmId* 获得。

