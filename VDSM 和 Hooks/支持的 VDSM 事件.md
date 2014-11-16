# 支持的 VDSM 事件

|事件名|说明|
|------|----|
|before\_vm\_start|虚拟机启动之前|
|after\_vm\_start|虚拟机启动之后|
|before\_vm\_cont|虚拟机继续运行之前（从暂停状态恢复）|
|after\_vm\_cont|虚拟机继续运行之后|
|before\_vm\_pause|虚拟机暂停之前|
|after\_vm\_pause|虚拟机暂停之后|
|before\_vm\_hibernate|虚拟机休眠之前|
|after\_vm\_hibernate|虚拟机休眠之后|
|before\_vm\_dehibernate|虚拟机从休眠状态恢复之前|
|after\_vm\_dehibernate|虚拟机从休眠状态恢复之后|
|before\_vm\_migrate\_source|虚拟机迁移之前，在发生迁移的源主机上运行。|
|after\_vm\_migrate\_source|虚拟机迁移之后，在发生迁移的源主机上运行。|
|before\_vm\_migrate\_destination|虚拟机迁移之前，在发生迁移的目标主机上运行。|
|after\_vm\_migrate\_destination|虚拟机迁移之后，在发生迁移的目标主机上运行。|
|after\_vm\_destroy|虚拟机销毁之后|
|before\_vdsm\_start|VDSM 在主机上启动之前。*before\_vm\_start* Hook 将使用 root 用户运行，并且不从 VDSM 进程中继承运行环境。|
|after\_vdsm\_stop|VDSM 在主机上停止之后。*after\_vdsm\_stop* Hook 将使用 root 用户运行，并且不从 VDSM 进程中继承运行环境。|
|before\_nic\_hotplug|虚拟机热添加网卡之前|
|after\_nic\_hotplug|虚拟机热添加网卡之后|
|before\_nic\_hotunplug|虚拟机热删除网卡之前|
|after\_nic\_hotunplug|虚拟机热删除网卡之后|
|after\_nic\_hotplug\_fail|虚拟机热添加网卡失败之后|
|after\_nic\_hotunplug\_faile|虚拟机热删除网卡失败之后|
|before\_disk\_hotplug|虚拟机热添加磁盘之前|
|after\_disk\_hotplug|虚拟机热添加磁盘之后|
|before\_disk\_hotunplug|虚拟机热删除磁盘之前|
|after\_disk\_hotunplug|虚拟机热删除磁盘之后|
|after\_disk\_hotplug\_fail|虚拟机热添加磁盘失败之后|
|after\_disk\_hotunplug\_fail|虚拟机热删除磁盘失败之后|
|before\_device\_create|虚拟机网卡设备创建之前|
|after\_device\_create|虚拟机网卡设备创建之后|
|before\_update\_device|虚拟机网卡设备更新之前|
|after\_update\_device|虚拟机网卡设备更新之后|
|before\_device\_destroy|虚拟机网卡设备销毁之前|
|after\_device\_destroy|虚拟机网卡设备销毁之后|
|before\_device\_migrate\_destination|设备迁移之前，在发生迁移的目标主机上运行。|
|after\_device\_migrate\_destination|设备迁移之后，在发生迁移的目标主机上运行。|
|before\_device\_migrate\_source|设备迁移之前，在发生迁移的源主机上运行。|
|after\_device\_migrate\_source|设备迁移之后，在发生迁移的源主机上运行。|

