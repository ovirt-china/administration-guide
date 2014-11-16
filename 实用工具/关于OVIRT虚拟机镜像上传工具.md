# 关于OVIRT虚拟机镜像上传工具

使用*engine-image-uploader*工具可以查看export存储域的列表，上传OVF格式的虚拟机镜像文件到指定export存储域。OVIRTMANAGER能够识别和使用上传的虚拟机镜像。engine-image-uploader目前只支持在OVIRTMANAGER中导出的经过gzip压缩的虚拟机镜像。

使用虚拟机镜像上传工具极大地简化了分发虚拟机镜像的工作。

虚拟机镜像的格式包含以下内容：

    |-- images
    |   |-- [Image Group UUID]
    |        |--- [Image UUID (this is the disk image)]
    |        |--- [Image UUID (this is the disk image)].meta
    |-- master
    |   |---vms
    |       |--- [UUID]
    |             |--- [UUID].ovf

