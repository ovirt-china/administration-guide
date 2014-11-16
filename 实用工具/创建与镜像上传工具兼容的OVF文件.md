# 创建与镜像上传工具兼容的OVF文件

创建可以使用engine-image-uploader上传的OVF文件。

在MANAGER中创建一个空Export存储域。

将虚拟机导出到新创建的Export存储域。

登录到Export存储域所在的实际服务器，找到Export存储域对应的NFS共享目录，该目录下应该有2个目录：*images*和*master*。

执行以下命令：

    # tar -zcvf my.ovf ../images/ master/


使用生成的ovf文件即可在OVIRTMANAGER中恢复虚拟机。

创建的ovf文件，可以通过*engine-image-uploader*命令上传到OVIRTMANAGER进行虚拟机导入。
