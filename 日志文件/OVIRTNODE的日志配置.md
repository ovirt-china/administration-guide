# OVIRTNODE的日志配置

?

OVIRTNODE的配置界面中的Logging可以配置将日志信息传输到远程服务器。

logrotate简化了对于日志文件的管理。OVIRTNODE中日志文件的大小到达指定限制时会自动进行轮转操作。

logrotate会将日志文件重命名，并新建一个使用原来文件名的空日志文件。配置界面中的“Logrotate
Max LogSize”中配置的数值，决定日志文件是否需要轮转。

“Logrotate Max Log Size”中数值的单位是kb，默认值为1024。

rsyslog是OVIRTNODE上使用的日志服务程序。通过配置rsyslog，可以将OVIRTNODE的日志传输到远程服务器上。

1.  在“Server Address”中填入远程日志服务器的地址（ip或者域名、主机名）。

2.  在“Server
    Port”中填入远程日志服务器日志服务程序的监听端口，默认为514。

netconsole可以将内核信息传输到远程日志服务器。

1.  在“Server Address”中填入远程日志服务器的地 址。

2.  在“Server Port”中填入远程日志服务器日志服
    务程序的监听端口，默认为6666。

选中“Save”，敲击回车键保存配置。

OVIRTNODE上日志将会发送到远程日志服务器。

