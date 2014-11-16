# 使用 VDSM Hooking 模块

VDSM 包含了一个名为 hooking 的 Python 模块，该模块为 VDSM Hook
脚本提供了帮助函数。该模块作为一个例子提供，并且只对使用 Python 编写的
VDSM Hook 脚本有意义。

hooking 模块支持将虚拟机的 libvirt XML 读取到一个 DOM 对象中。Hook
脚本能够使用 Python 自带的 *xml.dom*
库（[](http://docs.python.org/release/2.6/library/xml.dom.html)）来对该对象进行操作。

被修改过的对象可以使用 hooking 模块的函数保存回至 libvirt XML 中。该
hooking 模块提供了一下的函数以支持 Hook 开发：

|函数名|参数|功能说明|
|------|----|--------|
|*tobool*|字符串|将字符串“true”或者“false”转换为布尔值|
|*read\_domxml*|-|将虚拟机的 libvirt XML 读取到一个 DOM 对象中|
|*write\_domxml*|DOM 对象|写入一个 DOM 对象到虚拟机的 libvirt XML|

