# engine-iso-uploader命令行参数说明

engine-iso-uploader的基本使用方法如下：

    engine-iso-uploader [options] list
    engine-image-uploader [options] upload [file].[file]...[file]


2种操作模式：list和upload。

-   list操作会列出OVIRTMANAGER中可用的ISO存储域。

-   upload操作会上传ISO镜像文件（可以是多个，多个ISO镜像文件之间使用空格分隔）到指定的ISO存储域。默认通过NFS共享目录上传，也支持使用SSH上传。

ISO镜像上传工具必须指定list或者upload其中一项操作，使用upload操作时，最少需要提供一个待上传镜像文件的路径。

engine-iso-uploader提供了一些参数对命令的行为进行控制。

--version
显示命令版本信息。

-h，--help
显示命令帮助信息。

--conf-file=配置文件路径
指定配置文件。

--quiet
启用该选项之后,将命令的输出减少到最少。该选项默认是不启用的。

-v，--verbose
启用该选项之后,命令将输出尽可能详细的信息。该选项默认是不启用的。

-f，--force
当目标存储域中已经存在一个和将要上传的文件名字相同，则必须使用强制模式。默认开启该选项。

-u 用户名，--user=用户名
指定上传文件时使用的用户名。用户名的格式为：user@domain。同时用户必须在OVIRTMANAGER中已经存在。

-r FQDN
指定目标OVIRTMANAGER服务器的FQDN域名。默认是localhost，即运行该命令的服务器和OVIRTMANAGER是同一台服务器。

指定ISO镜像文件上传的目标ISO存储域，下面的2个选项互斥，不能同时使用。

-i，--iso-domain=ISO存储域
指定ISO镜像文件上传的目标ISO存储域。

-n，--nfs-server=NFS共享目录
指定ISO镜像文件上传的目标NFS共享目录。

ISO镜像上传工具默认使用NFS共享上传文件，使用下面的选项可以切换为使用SSH连接上传。

--ssh-user=用户名
指定上传使用的SSH用户。

--ssh-port=SSH服务端口
指定远端服务器的SSH监听端口。

-k 公钥文件，--key-file=公钥文件
指定SSH连接的公钥文件。不使用公钥验证时，会提示输入指定SSH用户的密码。
