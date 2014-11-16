# OVIRTMANAGER配置项的说明、限制以及配置建议

|配置项|说明|数据类型|建议值（或者默认值）|备注|
|------|----|--------|--------------------|----|
|AsyncTaskPolling​Rate|异步事务轮询频率|整数|10|OVIRTMANAGER查询异步事务状态的频繁程度|
|AsyncTaskZombie​TaskLifeInMinutes|僵尸事务的生命周期（分钟）|整数|3000|事务执行多长时间之后会被认为是僵尸事务并被杀死。该配置对大规模存储操作的影响需要特别考虑。如果存储设备速度较慢而虚拟镜像体积较大，或者事务运行时间超过3000分钟（50个小时），需要适量增大该配置。|
|AttestationPort|attestation服务的端口|整数|8443|attestation服务的监听端口。|
|AttestationServer|attestation服务器的fqdn域名|字符串|默认是“oat-server”|attestation服务器的fqdn域名或者ip地址。|
|AttestationTrustst​ore|和attestation服务器进行加密通信时使用的truststore文件。|字符串|TrustStore.jks|将attestation服务器*/var/lib/oat-appraiser/Certificate/*目录下的TrustStore.jks文件复制到MANAGER服务器的*/usr/share*目录下。|
|AttestationTrustst​orePass|访问truststore的密码|字符串|password|默认的密码是password。|
|AttestationFirstSta​geSize|第一阶段attestation的容量|整数|10|快速初始化时使用的配置。除非有明确的原因，否则不建议修改该配置。|
|AuditLogAgingThr​eshold|审计日志保存时限（以天为单位）|整数|30|审计日志在截断轮转之前最长的保存时限。|
|AuditLogCleanupT​ime|检查审计是否需要清理的时间|时间|03:35:35|检查审计日志是否超过时限以及是否需要清理。|
|AuthenticationMet​hod|OVIRTMANAGER中用户的验证方式|字符串|LDAP|OVIRTMANAGER验证用户的方式，目前支持LDAP。|
|BlockMigrationOn​SwapUsagePerce​ntage|NODE服务器swap使用率的限制（作为调度的依据）|整数|0|NODE服务器上允许虚拟机运行或者迁移消耗的最大swap使用率。如果服务器上swap使用率超过上限，虚拟机或者虚拟机迁移不会启动。|
|BootstrapMinimalV​dsmVersion|支持的VDSM最低版本|字符串|4.9|将主机加入到MANAGER时，主机上安装的VDSM版本必须不低于配置项指定的版本。新版本的VDSM特性更丰富。|
|CABaseDirectory|CA证书的目录|字符串|/etc/pki/ovirt-​engine|OVIRTMANAGER服务器上CA证书所在的目录。|
|CertificateFileNam​e|证书文件的名称|字符串|/etc/pki/ovirt-​engine/certs/engin​e.cer|OVIRTMANAGER进行SSL/TSL通信时使用的证书文件。|
|CpuOverCommitD​urationMinutes|CPU使用率超过集群调度策略的上限时，等待多长时间才开始进行实际的调度操作（时间以分钟为单位）。|整数|2|当集群调度策略设置为even时，如果检测到主机CPU使用超过配置上限，MANAGER会等待配置项设置的一段时间之后才开始进行虚拟机迁移。|
|DisableFenceAtSt​artupInSec|在OVIRTMANAGER启动时禁用fence操作一段时间（以秒为单位）|整数|300|OVIRTMANAGER启动时对主机进行检测，如果主机没有响应的时间超过该配置项设置的值，则认为主机的状态为不可操作，并开始执行fence操作。如果MANAGER服务器处于低速的网络环境，则需要考虑适量增大该配置。|
|WANDisableEffect​s|使用SPICE连接虚拟机时关闭WAN特效|多个字符串|animation|使用SPICE连接虚拟机时要关闭哪些特效。目前支持的值有：animation、​wallpaper、​font-smooth和all。|
|WANColorDepth|使用SPICE连接虚拟机时使用的色深|整数|16|使用SPICE连接虚拟机时使用的色深，可以配置的值有16和32。|
|EnableSpiceRoot​CertificateValidatio​n|是否启动SPICE客户端的根证书验证|字符串|true|如果配置项的值为“true”，当客户端通过SPICE连接虚拟机时，虚拟机所在主机的证书以及MANAGER的CA证书都会发送到客户端，目的是提供额外的安全认证机制。|
|EnableUSBAsDef​ault|是否自动将USB设备附加到虚拟机|字符串|true|-|
|EnableVdsLoadBa​lancing|是否启用NODE负载均衡|字符串|true|该配置项可以配置是否根据集群策略中配置的规则来进行虚拟机的负载均衡调度。|
|FreeSpaceCritical​LowInGB|磁盘剩余空间警告阈值（以GB为单位）|整数|5|当存储域的剩余空间减少到配置项指定的数值时产生一个警告。该配置项也会在判断存储相关操作是否会超过这个限制的过程中产生作用。添加或者导出磁盘镜像会因为剩余空间不足而失败。|
|FreeSpaceLow|磁盘剩余空间百分比低于配置值时会被认为是空间不足|整数|10|当存储域的剩余空间百分比减少到配置项指定的数值时，认为空间不足。|
|HighUtilizationFor​EvenlyDistribute|使用even负载均衡策略时，运行虚拟机数目的上限|整数|75|使用even负载均衡策略时，每台主机运行虚拟机的最大数量。|
|HighUtilizationFor​PowerSave|使用PowerSave负载均衡策略时，主机CPU使用率的上限|整数|75|对于新创建的集群生效，使用PowerSave负载均衡策略时，主机CPU使用率的上限。|
|LDAPQueryTimeo​out|LDAP查询超时时间|整数|30|LDAP查询的超时限制，超过配置项指定的时间之后查询会被终止。|
|LDAPOperationTi​meout|LDAP搜索操作的超时时间|整数|30|LDAP搜索操作的超时限制，超过配置项指定的时间之后搜索操作会被终止。|
|LDAPConnectTim​eout|LDAP查询时连接的超时时间|整数|30|LDAP查询时连接LDAP服务器的超时限制，超过配置项指定的时间之后，连接会被终止。|
|LocalAdminPassw​ord|admin@local用户的密码|密码|MANAGER安装时设置|admin@local用户的密码|
|LogPhysicalMemo​ryThresholdInMB|主机被认为内存不足的剩余内存下限（以MB为单位）|整数|1024|主机剩余内存低于配置项指定的数值时，会被认为是内存不足。当主机剩余内存低于下限时，该事件会记录到审计日志，不会对主机本身进行任何其他操作。|
|LowUtilizationForE​venlyDistribute|使用even负载均衡策略时，运行虚拟机数目的下限|整数|0|使用even负载均衡策略时，每台主机运行虚拟机的最小数量。|
|LowUtilizationForP​owerSave|使用PowerSave负载均衡策略时，主机CPU使用率的下限|整数|20|对于新创建的集群生效。使用PowerSave负载均衡策略时，主机CPU使用率的下限。|
|MacPoolRange|MAC地址区间|字符串|00:1a:4a:f1:3a:00​ -​ 00:1a:4a:f1:3a:ff|虚拟机网卡的MAC地址从配置项指定的地址区间中分配。|
|MaxMacsCountInP​ool|MAC地址区间中MAC地址数量的上限|整数|100000|MAC地址区间中MAC地址数量的上限。|
|MaxNumberofHost​sInStoragePool|存储域中主机的最大数量|整数|250|一个数据中心中添加的主机数量的上限。如有需要，经过测试之后，可以增加配置项指定的数值。|
|MaxNumOfCpuPer​Socket|虚拟机中一个Socket中CPU核心的上限|整数|16|虚拟机中，一个Socket中分配虚拟CPU核心的上限。|
|MaxNumOfVMCpu​s|虚拟机中虚拟CPU核心数量的上限|整数|160|单台虚拟机分配虚拟CPU核心的上限（虚拟机CPU核心的数量，等于每个Socket中CPU核心的数量乘以Socket的数量)。|
|MaxNumofVmSock​ets|虚拟机中Socket数量的上限|整数|16|单台虚拟机中CPU Socket数量的上限。|
|MaxRerunVmOnV​dsCount|虚拟机在一台主机上尝试重新运行次数的上限|整数|3|虚拟机在主机上尝试重新运行次数的上限，重试次数超过上限之后，主机会提示虚拟机无法运行的错误信息。|
|MaxScheduler​Weight|单一调度模块权值的上限|整数|1000|单一调度模块权值的上限。|
|MaxStorageVdsD​elayCheckSec|检查存储域状态的最大延时时间（以秒为单位）|整数|5|将确认存储域状态异常之前等待检测结果返回的最大延时时间。|
|MaxStorageVdsTi​meoutCheckSec|存储最后一次状态检测超时时间的上限|整数|30|检测存储域状态时，vdsmd会为每一个存储域设置一个“lastCheck”值。如果lastCheck对应的时间距离当前时间超过了配置项指定的数值，则存储域被认为是异常状态。|
|MaxVDSMeMOver​Commit|主机运行虚拟桌面时内存overcommit比例的上限|整数|200|主机运行虚拟桌面时，内存overcommit比例的上限。|
|MaxVdsMemOver​CommitForServers|主机运行虚拟服务器时内存overcommit比例的上限|整数|150|主机运行虚拟服务器时，内存overcommit比例的上限。|
|MaxVdsNameLen​gth|主机名称的最大长度|整数|255|主机名称的最大长度|
|MaxVmNameLengt​hNonWindows|非Windows平台虚拟机的名称的最大长度|整数|64|非Windows平台虚拟机的名称的最大长度|
|MaxVmNameLengt​hWindos|Windows平台虚拟机的名称的最大长度|整数|15|Windows平台虚拟机的名称的最大长度|
|MaxVmsInPool|数据中心虚拟机数量的上限|整数|1000|单一数据中心中虚拟机数量的上限。|
|VmPoolMaxSubse​quentFailures|使用虚拟机池时虚拟机创建失败次数的上限|整数|3|使用虚拟机池时新建虚拟机失败次数的上限。虚拟机失败次数超过限制，操作会被终止。|
|NumberOfVmsFor​TopSizeVms|存储域的虚拟机列表中显示的虚拟机数量（按虚拟机磁盘大小排序）|整数|10|存储域的虚拟机标签中，按照使用磁盘空间大小排序对虚拟机进行列表。列表中最多显示配置项指定数目的虚拟机。|
|NumberVmRefre​hesBeforeSave|在虚拟机数据写入到数据库之前允许的刷新次数|整数|5|2次从VDSM重新载入虚拟机信息之间主机监控操作的次数。每次主机监控操作都是根据该配置项指定的数值确定是否需要重新加载虚拟机信息。|
|oVirtISOsReposito​ryPath|OVIRTNODE安装文件的路径|字符串|/usr/share/ovirt​-node-iso|升级OVIRTNODE时使用的ISO镜像文件的路径。|
|ProductKey2003|产品序列号（Windows 2003）|字符串|-|使用sysprep创建Windows虚拟机模板使用的产品序列号。|
|ProductKey2003x​64|产品序列号（Windows 2003 x64）|字符串|-|使用sysprep创建Windows虚拟机模板使用的产品序列号。|
|ProductKey2008|产品序列号（Windows 2008）|字符串|-|使用sysprep创建Windows虚拟机模板使用的产品序列号。|
|ProductKey2008​R2|产品序列号（Windows 2008 R2）|字符串|-|使用sysprep创建Windows虚拟机模板使用的产品序列号。|
|ProductKey2008​x64|产品序列号（Windows 2008 x64）|字符串|-|使用sysprep创建Windows虚拟机模板使用的产品序列号。|
|ProductKey|产品序列号（Windows XP）|字符串|-|使用sysprep创建Windows虚拟机模板使用的产品序列号。|
|ProductKeyWindo​w7|产品序列号（Windows 7）|字符串|-|使用sysprep创建Windows虚拟机模板使用的产品序列号。|
|ProductKeyWindo​w7x64|产品序列号（Windows 7 x64）|字符串|-|使用sysprep创建Windows虚拟机模板使用的产品序列号。|
|ProductRPMVersi​on|OVIRTMANAGER软件包版本|字符串|自动从软件包中获取|当前使用的OVIRTMANAGER软件包版本。|
|SANWipeAfterDel​ete|创建虚拟磁盘时重新初始化更安全，但是IO所花费的时间较长（根据磁盘大小情况而定）。|字符串|false|该配置项会影响新建虚拟磁盘时是否选中“删除后清理”（新建虚拟磁盘在SAN类型的存储域中时）。|
|SASL\_QOP|用户认证或者LDAP查询时SASL的QoP级别|字符串|auth-conf|可选择的QoP等级有：auth，auth-int，auth-conf。|
|SearchResultsLimi​t|搜索结果条目数量的上限|整数|100|使用web管理门户或者REST api执行查询（没有特殊参数）时，搜索结果条目数量的上限。|
|SecureConnection​WithOATServers|访问attestation服务器时是否使用安全连接|布尔值|true||
|ServerRebootTim​eout|主机重启的超时时间限制（以秒为单位）|整数|300|当主机重启或者被fence时，如果主机在配置项指定的时间限制之前没有相应，则主机被认为是“NonResponsive”状态。如果主机重启时间较长，可以适量调整该配置。|
|SpiceProxyDefault|SPICE代理服务器的地址|字符串|无|该配置项配置之后，SPICE代理会自动开启。没有设置，则不会使用SPICE代理。|
|SpiceSecureChan​nels|SPICE安全通道|字符串|smain,sinputs,​scursor,splayback,​ srecord,sdisplay,​susbredir,ssmartcard|配置项中列出的SPICE通道会使用SSL安全连接。|
|SpiceReleaseCur​sorKeys|从SPICE客户端中释放鼠标的按键组合|字符串|Shift F12|-|
|SpiceUsbAutoSha​re|默认开启SPICE连接的USB设备共享|字符串|true|用户门户中SPICE客户端选项中的“启动USB自动共享”是否默认选中。|
|SpmCommandFail​OverRetries|SPM切换失败的重试次数|整数|3|SPM切换失败的重试次数。如果SPM指令失败，后台会开始尝试切换SPM，失败的指令会在新的SPM上重新执行。|
|SpmFailOverAttem​pts|SPM切换前重新尝试连接的次数|整数|3|监控存储域时，如果当前的SPM失效，不会立即进行切换。首先尝试重新连接当前的SPM，如果重试超过该配置指定的数值，则认为SPM已经停止运行，必须进行失效切换。|
|SpmVCpuConsum​ption|作为SPM的主机额外使用的虚拟CPU的数目|整数|1|作为SPM的主机，可以使用该配置项指定数值的额外虚拟CPU，以满足SPM操作产生的开销。|
|SSHInactivityHard​TimeoutSeconds|SSH连接无活动的超时时间（以秒为单位），最大限制|整数|1800|-|
|SSHInactivityTime​outSeconds|SSH连接无活动的超时时间（以秒为单位）|整数|600|SSH连接没有活动的时间超过配置项指定的数值时，会话会被终止。|
|NumberOfUSBSlots|虚拟机使用native的USB支持模式时，USB接口的数目|整数|4|-|
|SSLEnabled|SPICE使用是否SSL安全连接|字符串|true|SPICE安全通道是否使用SSL安全连接。|
|StorageDomainFai​lureTimeoutInMinu​tes|存储域失效的超时时间|整数|5|VDSM首次发现存储域故障之后，经过配置项指定的时间（以分钟为单位）之后仍然没有恢复，则认为存储域不可用。|
|StoragePoolRefre​shTimeInSeconds|检测存储域状态的间隔时间，以秒为单位|整数|10|检测存储域状态的频率。|
|SysPrep2K3Path|Windows 2003虚拟机对应的sysrep文件路径|字符串|/etc/ovirt​-engine/gsysprep/sys​prep.2k3|特定操作系统对应的sysprep文件模板的路径。|
|SysPrep2K8Path|Windows 2008虚拟机对应的sysrep文件路径|字符串|/etc/ovirt​-engine/gsysprep/sys​prep.2k8x86|特定操作系统对应的sysprep文件模板的路径。|
|SysPrep2K8R2Pat​h|Windows 2008 R2虚拟机对应的sysrep文件路径|字符串|/etc/ovirt​-engine/gsysprep/sys​prep.2k8|特定操作系统对应的sysprep文件模板的路径。|
|SysPrep2K8x64P​ath|Windows 2008虚拟机对应的sysrep文件路径|字符串|/etc/ovirt​-engine/gsysprep/sys​prep.2k8|特定操作系统对应的sysprep文件模板的路径。|
|SysPrepWindows​7Path|Windows 7虚拟机对应的sysrep文件路径|字符串|/etc/ovirt​-engine/gsysprep/sys​prep.w7|特定操作系统对应的sysprep文件模板的路径。|
|SysPrepWindows​7x64Path|Windows 7 x64虚拟机对应的sysrep文件路径|字符串|/etc/ovirt​-engine/gsysprep/sys​prep.w7x64|特定操作系统对应的sysprep文件模板的路径。|
|SysPrepWindows​8Path|Windows 8虚拟机对应的sysrep文件路径|字符串|/etc/ovirt​-engine/gsysprep/sys​prep.w8|特定操作系统对应的sysprep文件模板的路径。|
|SysPrepWindows​8x64Path|Windows 8 x64 虚拟机对应的sysrep文件路径|字符串|/etc/ovirt​-engine/gsysprep/sys​prep.w8x64|特定操作系统对应的sysprep文件模板的路径。|
|SysPrepWindows​2012x64Path|Windows 2012 x64虚拟机对应的sysrep文件路径|字符串|/etc/ovirt​-engine/gsysprep/sys​prep.2k12x64|特定操作系统对应的sysprep文件模板的路径。|
|SysPrepXPPath|Windows XP虚拟机对应的sysrep文件路径|字符串|/etc/ovirt​-engine/gsysprep/sys​prep.xp|特定操作系统对应的sysprep文件模板的路径。|
|TimeoutToResetV​dsInSeconds|通信超时时间，超过该时间开始尝试重置|整数|60|主机无响应的时间超过配置项指定的时间之后，开始执行fence操作。该配置项一般和VDSAttemptsTo​ResetCount一起使用。|
|DelayResetForSp​mInSeconds|对于SPM主机，重置操作的延时时间|双精度小数|20|-|
|DelayResetPerVm​InSeconds|重置虚拟机之前的延时时间|双精度小数|0.5|-|
|TimeToReduceFai​ledRunOnVdsInMi​nutes|主机上运行虚拟机失败后处于“错误”状态的时间（以分钟为单位）|整数|30|主机上运行虚拟机失败后处于“错误”状态的时间。|
|UserDefinedVMPr​operties|用户自定义的虚拟机属性|字符串|用户自定义|用于实现用户的特殊需求。|
|UserRefreshRate|AD用户数据的刷新间隔时间（以秒为单位）|整数|3600|更新AD用户数据信息的间隔时间。|
|UtilizationThre​sholdInPercent|CPU使用率的阈值（百分比）|整数|80|负载均衡策略中，判断主机负载是否过高的标准（CPU使用率方面）。该配置项可以在集群的策略配置对话框中进行配置。|
|ValidNumOfMonito​rs|显示设备的可选数量|整数|1，2，4|启动SPICE连接的虚拟机显示设备的数量。|
|VdcVersion|OVIRT内部版本号|字符串|安装时自动设置|-|
|VDSAttemptsToRe​setCount|重置主机之前尝试重新连接的次数|整数|2|在对主机发起fence操作之间尝试重新连接主机的次数，该配置项和TimeoutToReset​VdsInSeconds配合使用。|
|VdsLoadBalancin​geIntervalInMinutes|主机负载均衡状态检查间隔（以分钟为单位）|整数|1|根据主机负载情况对虚拟机运行情况做出调整的时间间隔。（该配置项也是第一次进行负载均衡调度的时间）|
|VdsRecoveryTime​outInMintues|主机恢复时的超时时间（以分钟为单位）|整数|3|等待主机恢复正常状态的超时时间（主机状态一般显示为“初始化”或者“恢复”。|
|VdsRefreshRate|获取主机状态信息的间隔时间（以秒为单位）|整数|2|获取主机状态信息的间隔时间（以秒为单位）|
|vdsTimeout|主机通信异常的超时时间（以秒为单位）|整数|180|主机通信异常的超时时间（以秒为单位）|
|vdsConnectionTi​meout|与主机建立连接时的超时时间（以秒为单位）|整数|2|与主机建立连接时的超时时间（以秒为单位）|
|vdsRetries|与主机通信失败时重新尝试的次数|整数|0|与主机通信失败时重新尝试的次数|
|VmGracefulShutd​ownMessage|在管理中心关闭虚拟机时，虚拟机中显示的提示信息|字符串|System Administrator has initiated shutdown of this Virtual Machine. Virtual Machine is shutting down.|-|
|VMMinMemorySize​InMB|虚拟机内存容量的下限（以MB为单位）|整数|256|-|
|VM32BitMaxMemor​ySizeInMB|32位平台虚拟机内容容量的最大值（以MB为单位）|整数|20480|-|
|VM64BitMaxMemor​ySizeInMB|64位平台虚拟机内容容量的最大值（以MB为单位）|整数|524288，2097152，​2097152，2097152（针对不同兼容版本时存在差异）|-|
|VncKeyboardLayo​ut|使用VNC连接虚拟机时的键盘布局|字符串|en-US|可用的键盘布局有：ar， da， de-ch， en-us， et，fo， fr-be， fr-ch， hu， it， li， mk， nl，no， pt， ru， sv， tr， deen-gb， es， fi，fr， fr-ca， hr， is， ja， lv， nl-be， pl，pt-br， sl， th.|
|WaitForVdsInitI​nSec|在SPM选举中等待主机完成初始化的超时时间（以秒为单位）|整数|60|该配置项和VdsRecoveryTim​eoutInMinutes类似，不同的是适用于SPM选举过程中，而且时间更短。如果选中的SPM主机在进行初始化，会等待其进入正常状态。|
|FenceQuietTimeB​etweenOperations​InSec|2次电源管理操作的间隔时间（以秒为单位）|整数|180|用户手动执行电源操作时，2次操作之间的最短间隔时间。|
|FenceProxyDefau​ltPreferences|fence操作中代理服务的默认属性|字符串|cluster，dc|fence操作中，代理服务的默认属性，定义如何搜索代理服务。|
|MaxAuditLogMess​ageLength|审计日志长度的上限|整数|1000|-|
|SysPrepDefaultUser|sysprep默认用户|字符串|-|进行sysprep操作时域未知或者未指定时，使用该配置项指定的用户。|
|SysPrepDefaultP​assword|默认你的sysprep用户密码|密码|Empty|进行sysprep操作时域未知或者未指定时，使用该配置项指定的用户密码。|
|UserSessionTime​OutInterval|用户会话的超时时间（以分钟为单位）|整数|30|用户会话的超时时间（对于所有的登录方式都生效：用户门户、管理门户，API等）。|
|UserSessionTime​OutInvalidatio​nInterval|验证用户会话是否超时的间隔时间（以分钟为单位）|整数|30|验证用户会话是否超时的间隔时间（以分钟为单位）|
|AdminPassword|admin@local用户的密码|密码|\*\*\*\*\*\*|admin@local用户的密码。|
|IPTablesConfig|安装管理中心时自动配置的防火墙规则|字符串||安装管理中心时自动配置的防火墙规则|
|OvirtIsoPrefix|oVirt光盘镜像文件名的前缀|字符串|ovirt-node||
|OvirtInitialSup​portedIsoVersion|支持的oVirt node光盘镜像的最低版本|字符串|2.5.5||
|VdsLocalDisksLo​wFreeSpace|主机上磁盘剩余空间的阈值，剩余空间小于此值时，主机被认为是剩余磁盘空间低，以MB为单位|整数|1000|如果设置为低于1000的值，会导致在为数据中心增加存储空间之前虚拟机的性能开始下降。如果数据中心中有大量虚拟机在生成和接受数据，应该适量增大该配置项的数值。|
|VdsLocalDisksCr​iticallyLowFree​Space|当主机剩余磁盘空间低于该值时，必须立刻采取措施（以MB为单位）|整数|500|如果设置为低于500的值，会导致在为数据中心增加存储空间之前虚拟机的性能开始下降。如果数据中心中有大量虚拟机在生成和接受数据，应该适量增大该配置项的数值。|
|AllowDuplicateM​acAddresses|是否允许虚拟机网卡的MAC地址重复|字符串|false|如果设置为true，同一个MAC地址可以在多个虚拟机中使用。默认情况，所有虚拟网卡的MAC都是唯一的。|
|JobCleanupRateI​nMinutes|事务清理操作的频率（以分钟为单位）|整数|10||
|SucceededJobCle​anupTimeInMinut​es|已成功执行事务的清理频率（以分钟为单位）|整数|10||
|FailedJobCleanu​pTimeInMinutes|执行失败的事务的清理频率（以分钟为单位）|整数|60||
|VmPoolMonitorIn​tervalInMinutes|监控虚拟机池中预启动虚拟机数目的时间间隔（以分钟为单位）|整数|5||
|VmPoolMonitorBa​tchSize|虚拟机池一个周期内预启动虚拟机的最大数目|整数|5||
|NetworkConnecti​vityCheckTimeou​tInSeconds|调整主机网络时，如果新的配置导致主机和管理中心之间的通信中断，超过配置项指定的时间之后，自动回滚到主机之前的配置，以秒为单位。|整数|120||
|AllowClusterWit​hVirtGlusterEna​bled|是否允许创建同时支持Virt和Gluster服务的集群|字符串|false|如果设置为true，允许用户创建同时Virt和Gluster服务的集群。|
|EnableMACAntiSp​oofingFilterRules|是否启用反MAC地址欺骗过滤|字符串|false，false，​true，true（针对不同兼容版本时存在差异）|如果启用反MAC地址欺骗，虚拟网卡发出的所有数据帧中都会包含MAC地址信息。|
|EnableHostTimeD​rift|是否启动主机的时间漂移检验|字符串|false|如果设置为true，管理中心会验证主机的时钟和自身的差异是否在可接受的范围之内。可接受的时间误差由HostTimeDriftInSec配置项设置。|
|EngineMode|管理中心的工作模式|字符串|Active|有效的工作模式有：Active， Maintenance，Prepare。|
|HostTimeDriftIn​Sec|管理中心和主机之间允许的时钟差异（以秒为单位）|整数|300||
|LogMaxPhysicalM​emoryUsedThresh​oldInPercentage|主机物理内存使用率的阈值，超过该限制之后，触发审计日志事件（百分比）|整数|95||
|LogMaxCpuUsedTh​resholdInPercen​tage|主机物理CPU使用率的阈值，超过该限制之后，触发审计日志事件（百分比）|整数|95||
|LogMaxNetworkUs​edThresholdInPe​rcentage|主机物理网卡使用率的阈值，超过该限制之后，触发审计日志事件（百分比）|整数|95||
|LogMinFreeSwapT​hresholdInMB|主机swap剩余空间的阈值，超过该限制之后，触发审计日志事件（以MB为单位）|整数|256||
|LogMaxSwapUsedT​hresholdInPerce​ntage|主机swap空间使用率的阈值，超过该限制之后，触发审计日志事件（百分比）|整数|95||
|ClientModeSpice​Default|SPICE客户端连接的默认模式|字符串|Auto|可选的模式有：Auto， Plugin， Native。|
|ClientModeRdpDe​fault|RDP客户端连接的默认模式|字符串|Auto|可选的模式有：Auto， Plugin， Native。|
|WebSocketProxy|WebSocket代理服务的地址|字符串|Engine:6100|地址的格式：Off（没有代理服务）、Host:端口号、Engine:端口号、主机名（或者ip地址）:端口号。|
|WebSocketProxyT​icketValiditySe​conds|WebSocket代理服务票证验证的间隔时间（以秒为单位）|整数|120||
|CustomDevicePro​perties|用户自定义的设备属性|字符串|||
|GlusterRefreshR​ateHooks|gluster hooks的刷新时间间隔（以秒为单位）|整数|7200||
|KeystoneAuthUrl|OpenStack KeyStone服务的URL地址|字符串|||
|DefaultWindowsT​imeZone|Windows虚拟机的默认时区|字符串|GMT Standard Time||
|DefaultGeneralT​imeZone|Linux及其他系统平台虚拟机的默认时区|字符串|Etc/GMT||
|OnlyRequiredNet​worksMandatoryF​orVdsSelection|选择虚拟机运行的主机时是否只考虑必需的网络|字符串|false|如果设置为true，选择虚拟机在哪一台主机上运行时，只考虑必需的网络。|
|MaxAverageNetwo​rkQoSValue|网络QoS的上限（以Mb/s为单位）|整数|1024||
|MaxPeakNetworkQ​oSValue|网络传输高峰时QoS的上限（以Mb/s为单位）|整数|2048||
|MaxBurstNetwork​QoSValue|网络传输突发时QoS的上限（以Mb/s为单位）|整数|10240||
|UserMessageOfTh​eDay|用户门户登录界面的友好提示信息|字符串|||
|QoSInboundAvera​geDefaultValue|网络接受数据时QoS数值（以Mb/s为单位）|整数|10||
|QoSInboundPeakD​efaultValue|网络接受数据（传输高峰期）时QoS数值（以Mb/s为单位）|整数|10||
|QoSInboundBurst​DefaultValue|网络接受数据（传输突发时）时QoS数值（以Mb/s为单位）|整数|100||
|QoSOutboundAver​ageDefaultValue|网络发送数据时QoS数值（以Mb/s为单位）|整数|10||
|QoSOutboundPeak​DefaultValue|网络发送数据（传输高峰期）时QoS数值（以Mb/s为单位）|整数|10||
|QoSOutboundBurs​tDefaultValue|网络发送数据（传输突发时）时QoS数值（以Mb/s为单位）|整数|100||
|SecureConnectio​nWithOATServers|访问attestation服务器时是否使用安全连接|字符串|true||
|PoolUri|attestation服务的地址|字符串|AttestationServ​ice/resources/P​ollHosts||
|ExternalSchedul​erServiceURL|外部调度服务的URL地址|字符串|http://localhos​t:18781/||
|ExternalSchedul​erConnectionTim​eout|访问外部调度服务的超时时间|整数|100|设置为0时可以取消超时时间的限制。|
|ExternalSchedulerEnabled|是否启动外部调度服务|布尔值|false||
|ExternalSchedul​erResponseTimeo​ut|外部调度服务响应的超时时间|整数|120000||
|DwhHeartBeatInt​erval|DWH心跳间隔时间（以秒为单位）|整数|30||
|UseFqdnForRdpIf​Available|RDP客户端连接是是否使用fqdn域名|布尔值|true|设置为“true”时，RDP客户端连接时会使用虚拟机Agent提供的虚拟机的fqdn域名（前提是虚拟机配置了fqdn域名）。|
|SpeedOptimizati​onSchedulingThr​eshold|负载均衡调度时启动speed优化的阈值|整数|10|负载均衡策略启用了speed优化之后，如果有超过配置项指定阈值的调度请求没有处理，则直接跳过对主机权值的计算，迅速完成调度。|
|SchedulerAllowO​verBooking|是否跳过可能引发overbooking的调度资源同步|布尔值|false||
|SchedulerOverBo​okingThreshold|忽略可能引发超额调度请求的调度资源同步的阈值|整数|10|如果SchedulerAllo​wOverBooking配置为“true”，而且集群允许overbooking，当出现大于配置项指定数值的调度情况没有处理时，则直接跳过调度资源同步的过程。|
|HostPreparingFo​rMaintenanceIdl​eTime|等待主机进去维护模式的延时时间|整数|300|在确认主机处于准备进去维护模式之前等待的延时时间。这段时间之后会将此触发将主机置于维护状态的操作。|

