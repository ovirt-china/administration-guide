# OVIRT支持的虚拟机操作系统

目前 OVIRT支持以下虚拟机操作系统:

|操作系统|架构|SPICE 支持|
|--------|----|----------|
|Red Hat Enterprise Linux 3(或CentOS 3)|32-bit，64-bit|是|
|Red Hat Enterprise Linux 4(或CentOS 4)|32-bit，64-bit|是|
|Red Hat Enterprise Linux 5(或CentOS 5)|32-bit，64-bit|是|
|Red Hat Enterprise Linux 6(或CentOS 6)|32-bit，64-bit|是|
|SUSE Linux Enterprise Server 10|32-bit，64-bit|否|
|SUSE Linux Enterprise Server 11|32-bit，64-bit|否|
|Ubuntu 12.04 (Precise Pangolin LTS)|32-bit，64-bit|是|
|Ubuntu 12.10 (Quantal Quetzal|32-bit，64-bit|是|
|Ubuntu 13.04 (Raring Ringtail)|32-bit，64-bit|是|
|Ubuntu 13.10 (Saucy Salamander)|32-bit，64-bit|是|
|Windows XP Service Pack 3 and newer|32-bit|是|
|Windows 7|32-bit，64-bit|是|
|Windows 8|32-bit，64-bit|否|
|Windows Server 2003 Service Pack 2 and newer|32-bit，64-bit|是|
|Windows Server 2008|32-bit，64-bit|是|
|Windows Server 2008 R2|64-bit|是|
|Windows Server 2012 R2|64-bit|否|

对 Windows 8 和 Windows 2012 来讲，默认使用 RDP(Remote Desktop Protocol)
作为访问协议，因为微软增加了一些新的改变到显示的协议上，这些改动导致
SPICE 暂时得不到最好的体验。

> **Note**
>
> 因为由于 Red Hat Enterprise Linux 3 and Red Hat Enterprise Linux 4
> 是32位内核，没有 ACPI
> 的支持，所以用户在门户直接点击关闭的时候肯能会出现
> 问题，这个时候需要用户右击断电来关机。

