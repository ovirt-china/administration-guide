# ISO镜像上传工具基本使用示例

下面是ISO镜像上传工具的基本使用方法的示例。第一条命令列出了OVIRTMANAGER中可用的ISO存储域，使用的用户是admin@local。第二条命令通过NFS共享将ISO镜像文件上传到了指定的ISO存储域。

    # engine-iso-uploader list
    Please provide the REST API password for the admin@internal oVirt Engine user
    (CTRL+D to abort):
    ISO Storage Domain Name   | Datacenter                | ISO Domain Status
    ISO-DOMAIN                | Default                   | active
    ISO_DOMAIN                | iscsi                     | active
    ISO_DOMAIN                | local_datacenter          | active


    # engine-iso-uploader --iso-domain=[ISODomain] upload \
    [CentOS-6.5-x86_64.iso]
    Please provide the REST API password for the admin@internal oVirt Engine user
    (CTRL+D to abort):

