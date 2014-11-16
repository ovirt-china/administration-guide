# VDSM Hook 的执行

*before\_vm\_start* 脚本能够编辑 libvirt domain XML 以在到达 libvirt
之前修改 VDSM 关于一个虚拟机的定义。这么做的时候必须十分谨慎。Hook
脚本有可能妨碍 VDSM 的正常工作，存在问题的脚本将有可能使得 OVIRT
虚拟化环境不正常。尤其需要注意的是，请确保您不会改变该虚拟机的
UUID，也不要在没有足够的相关背景知识的情况下尝试在脚本中删除虚拟机上的一个设备。

*before\_vdsm\_start* 和 *after\_vdsm\_stop* Hook 脚本都是以 *root*
用户运行的。其它执行过程中需要使用 *root*
权限的脚本则必须被添加到能够使用 `sudo`
命令提升权限执行的列表之中。为达到这个目地，`/etc/sudoers`
文件必须被更新以允许 *vdsm* 用户不需要重新输入密码就能够使用 `sudo`
命令。这些操作是必需的，因为 Hook 脚本是非交互式地执行。

在这个例子中我们将会修改 `sudo` 命令的配置以允许 *vdsm* 用户以 *root*
用户权限执行 `/bin/chown`。

1.  使用 *root* 账户登录到虚拟化主机中。

2.  在文本编辑器中打开 `/etc/sudoers` 文件。

3.  添加如下一行到该文件中：

        vdsm ALL=(ALL) NOPASSWD: /bin/chown


    这将指定 *vdsm* 用户能够以 *root* 用户权限执行 `/bin/chown`
    命令。其中的 *NOPASSWD* 参数表示用户在使用 `sudo`
    的时候将不会被提示需要输入他们的密码。

一旦修改了该配置，VDSM Hook 将能够使用 `sudo` 以 *root* 用户权限执行
`/bin/chown`。下面所示的 Python 代码使用了 `sudo` 以 *root*
用户权限对文件 `/my_file` 执行了 `/bin/chown`。

    retcode = subprocess.call( ["/usr/bin/sudo", "/bin/chown", "root", "/my_file"])


