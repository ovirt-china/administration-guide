# engine-image-uploader使用示例

下面的示例使用*engine-image-uploader*列出存储域上传OVF文件：

    # engine-image-uplaoder list
    Please provide the REST API username for the admin@local oVirt Engine user:
    **********
    Export Storage Domain Name | Datacenter | Export Domain Status
    myexportdom                | Myowndc    | active


上传镜像文件时，需要指定NFS共享目录（-n选项）或者Export存
储域（-e选项），以及需要上传的文件名：

    # engine-image-uploader -e myexportdom upload my.ovf
    Please provide the REST API username for the admin@local oVirt Engine user:
    **********


