# OVIRT配置管理工具的命令行说明

OVIRTMANAGER服务器上安装了配置管理工具，关于命令的详细说明可以执行下面的命令获取：

    # engine-config --help


列出所有的配置项
使用*--list*选项可以列出所有的配置项

    # engine-config --list


所有的配置项及其描述都会打印出来。

列出所有配置项的值
使用*--all*选项可以列出所有配置项的值

    # engine-config --all


所有的配置项、配置项当前值以及配置版本都会打印出来。

获取指定配置项的值
使用*--get*可以获取指定配置项的值

    # engine-config --get KEY_NAME


将*KEY\_NAME*替换为要查询的配置项。命令会打印出该配置项，配置项当前值以及配置版本。要或者指定配置版本中配置项的值，需要加上*--cver*选项。

设置指定配置项的值
使用*--set*可以设置指定配置项的值，要设置指定配置版本中配置项的值，需要加上*--cver*选项。

    # engine-config --set KEY_NAME=KEY_VALUE --cver=VERSION

将*KEY\_NAME*替换为要设置的配置项，*KEY\_VALUE*替换为配置项的值，设置其他版本配置中的配置项时将*VERSION*替换为配置的版本。
