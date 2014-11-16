# engine-log-collector命令行参数说明

engine-log-collector的基本使用方法如下：

    engine-log-collector [options] list [all, clusters, datacenters]
    engine-image-uploader [options] collect


2种操作模式：list和collect。

-   list操作会列出OVIRTMANAGER中的数据中心、集群或者主机。

-   collect操作会从OVIRTMANAGER抓取相关的日志和信息，并打包放置在/tmp/logcollector目录下。

如果没有指定其他参数，默认的操作是自动收集当前MANAGER中所有数据中心、集群和主机相关的信息和日志，并打包。

engine-log-collector提供了一些参数对命令的行为进行控制。

--version
显示命令版本信息。

-h，--help
显示命令帮助信息。

--conf-file=配置文件路径
指定配置文件。

--local-tmp=收集日志文件的存放路径
指定收集到的日志文件的存放路径。默认的路径是：/tmp/logcollector。

--ticket-number=TICKET
指定ticket序号，主要用于区分生成的日志文件的名称。

--upload=FTP服务器
日志收集完成之后上传到指定的FTP服务器。

--log-file=日志文件路径
指定记录命令输出的日志文件。

--quiet
启用该选项之后，将命令的输出减少到最少。该选项默认是不启用的。

-v，--verbose
启用该选项之后，命令将输出尽可能详细的信息。该选项默认是不启用的。

下面这些选项可能指定访问OVIRTMANAGER时验证登录的方式、选择需要收集的日志或者信息的类型、来源等。

这些选项可以配合使用，如：engine-log-collector --user=admin@local
--cluster ClusterA,ClusterB --hosts
"SalesHost"\*，将使用admin@local登录MANAGER，并收集ClusterA和ClusterB这2个集群中所有SaleHost主机的日志和信息。

--no-hypervisors
不收机主机相关的日志和信息。

-u 用户，--user=用户
登录MANAGER时使用的用户。用户名的格式为：user@domain。同时用户必须在OVIRTMANAGER中已经存在。

-r FQDN
指定目标OVIRTMANAGER服务器的FQDN域名。默认是localhost，即运行该命令的服务器和OVIRTMANAGER是同一台服务器。

-c 集群，--cluster=集群
收集指定集群（可以是多个）相关的日志和信息。如果指定多个集群，集群名之间使用“,”分隔。支持使用通配符。

-d 数据中心，--datacenter=数据中心
收集指定数据中心（可以是多个）相关的日志和信息。如果指定多个数据中心，数据中心名之间使用“,“分隔。支持使用通配符。

-H 主机列表，--hosts=主机列表
收集指定主机（或者多个主机）相关的日志和信息。多个主机使用“,”分割，可以使用主机名、ip地址，fqdn域名，也支持使用通配符。

日志收集工具使用了JBoss SOS插件。使用下面的选项可以从JMX终 端收集信息。

--jboss-home=JBOSS\_HOME
JBoss的安装目录，默认是/var/lib/jbossas。

--java-home=JAVA\_HOME
Java的安装目录，默认是/usr/share/jvm/java。

--jboss-profile=JBOSS\_PROFILE
指定日志收集使用的Jboss Profile配置。

--enable-jmx
从OVIRTMANAGER的JMX接口获取日志和信息。

--jboss-user=JBOSS\_USER
调用JBoss JMX接口的用户，默认是admin。

--jboss-logsize=LOG\_SIZE
最终生成的日志文件的最大体积（单位为MB）。

--jboss-stdjar=STATE
是否收集JBoss标准JAR状态信息。STATE可选的值为on或者off，默认为on。

--jboss-servjar=STATE
是否收集所有服务配置目录下的JAR状态信息。STATE可选的值为on或者off，默认为on。

--jboss-twiddle=STATE
是否收集twiddle数据。STATE可选的值为on或者off，默认是on。

--jboss-appxml=XML\_LIST
指定需要收集的应用的XML描述。默认为all。

--ssh-port=端口
连接虚拟机时SSH服务的端口。

-k 公钥文件，--key-file=公钥文件
指定通过SSH连接虚拟机时使用的公钥文件。

--max-connections=最大连接数
设置与虚拟机之间的SSH连接的MAX\_CONNECTIONS参数，默认为10。

如果更改了OVIRTMANAGER数据库名和数据库用户，则需要在执库名和数据库用户。

如果数据库不再本地，则需要通过pg-hostdb指定数据库所在的服务器的日志，数据库需要安装SOS插件。

--no-postgresql
不收集数据库相关日志和信息。默认该选项没有开启。

--pg-user=数据库用户
指定连接数据库使用的用户。默认为postgres。

--pg-dbname=数据库名
指定连接到数据库服务器要访问的数据库，默认为engine。

--pg-dbhost=数据库服务器
指定数据库服务器。默认为localhost。

--pg-host-key=公钥文件
指定访问数据库时使用的公钥。当数据库服务器不在本地时，需要使用该选项。
