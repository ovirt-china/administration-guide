# OVIRT虚拟机镜像上传工具的命令行说明

engine-image-uploader的基本使用方法如下：

    engine-image-uploader [options] list
    engine-image-uploader [options] upload [file].[file]...[file]


2种操作模式：list和upload。

-   *list*操作会列出所有可以上传镜像的export存储域。

-   *upload*操作将指定的镜像文件上传到指定的存储域。

使用*engine-image-uploader*时必须指定*list*或者*upload*其中一种操作。进行*upload*操作时最少提供一个镜像文件名已进行上传。

其他的命令行参数可以对*engine-image-uploader*命令进行更精细的控制，也可以将一些默认的配置参数写入到配置文件：
*/etc/ovirt-engine/im ageuploader.conf*。

-h，--help
显示命令的帮助信息。

--config-file=配置文件路径
指定配置文件。默认的配置文件是*/etc/ovirt-engine/imageuploader.conf*。

--log-file=日志文件路径
指定命令执行过程中输出内容写入的日志文件。

--quiet
设置命令执行过程产生最少的输出内容。默认不开启 该选项。

--verbose
设置命令执行过程产生尽可能多的输出内容。默认不开启该选项。

-f，--force
当目标存储域中已经存在一个和将要上传的文件名字相同，则必须使用强制模式。默认开启该选项。

-u 用户名，--user=用户名
上传镜像文件时使用的用户。用户名的格式为：*user@domain*。同时用户必须在OVIRTMANAGER中已经存在。

-r FQDN
指定镜像文件上传的目标OVIRTMANAGER服务器的*FQDN*域名。默认是*localhost:443*，即运行该命令的服务器和OVIRTMANAGER是同一台服务器。

下面的选项指定镜像文件上传的目标Export存储域，这些选项是互
斥的，不能同时使用。

-e，--export-domain=Export存储域名称
指定镜像文件上传的目标*Export*存储域。

-n，-nfs-server=NFS共享目录地址
指定镜像文件上传的目标NFS共享目录地址。

-i，--ovf-id
开启该选项之后，镜像文件的UUID不会被修改。默认的情况下，镜像文件上传之后会自动获取一个新的UUID，不会和其他的UUID冲突。

-d，--disk-instance-id
开启该选项之后，镜像文件中所有磁盘的实例ID不会被修改。默认的情况下，镜像文件上传之后磁盘都会自动获取一个新的UUID防止出现冲突。

-m，--mac-address
开启该选项之后，镜像文件中的网络组件不会被删除。默认情况下镜像文件上传时其中的网络组件会被删除以防止和其他的网络设备发生冲突。

-N 新镜像文件名，--name=新镜像文件名
开启该选项之后，镜像文件上传之后会使用新的文件名。
