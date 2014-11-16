# 上传 ISO 到 ISO 域

*概述*.
OVIRT 管理平台提供了一个简单的脚本，用来上传 ISO 文件到 ISO
存储域，并设置合理的访问权限。

首先，复制需要上传的 ISO 文件到运行 OVIRT 管理平台的系统的临时目录下。

使用 *root* 用户登录到 OVIRT 管理平台系统。

使用 `engine-iso-uploader` 命令查看存在的 ISO 存储域的名字：

    # engine-iso-uploader list


使用 `engine-iso-uploader` 命令上传 ISO 文件：

    # engine-iso-uploader --iso-domain=ISO-DOMAIN upload /tmp/ovirt-node-iso-3.1.0-0.999.456.el6.iso


该命令需要一个 ISO
存储域的名称作为参数，使用上一步的命令获取，还需要输入 ISO
文件的完整路径，该命令会提示用户输入 REST API 的密码。

*结果*.
ISO 上传完成并出现在命令中指定的 ISO 存储域中。同时也将出现在创建该 ISO
存储域所附加到的数据中心中的虚拟机时可用的启动媒介列表中。

*参见：*

-   ?
