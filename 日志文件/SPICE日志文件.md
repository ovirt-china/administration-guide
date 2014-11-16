# SPICE日志文件

在整个OVIRT虚拟化环境中不同的地方都有SPICE相关的日志，包括客户端和虚拟机上。

|日志类型|日志未知|调整日志级别|
|--------|--------|------------|
|SPICE客户端（Windows 7）|%temp%\\spicex.log|-   右键点击主菜单的“我的电脑”，点击“属性”。

-   进入“高级”系统配置，点击“环境变量”。

-   找到“用户”或者“系统”变量，新建一个值为4的变量“SPICEX\_DEBUG\_LEVEL”。

|
|SPICE客户端（Windows XP）|C:\\Documents and Settings\\(User Name)\\Local Settings\\T emp\\spicex.log|-   右键点击主菜单的“我的电脑”，点击“属性”。

-   进入“高级”系统配置，点击“环境变量”。

-   找到“用户”或者“系统”变量，新建一个值为4的变量“SPICEX\_DEBUG\_LEVEL”。

|
|SPICE客户端（Linux）|/var/log/message|使用SPICE\_DEBUG=1 firefox启动Firefox浏览器。|
|OVIRTNODE上的SPICE服务进程|/var/log/libvirt/qemu/(虚拟机名称).log|启动虚拟机之前，首先执行export SPIECE\_DEBUG\_LEVEL=5。|

