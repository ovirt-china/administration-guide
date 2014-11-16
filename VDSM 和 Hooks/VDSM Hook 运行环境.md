# VDSM Hook 运行环境

大多数的的 Hook 脚本使用 *vdsm* 用户运行并且从 VDSM
进程中继承运行环境。有两个例外是分别由 *before\_vdsm\_start* 和
*after\_vdsm\_stop* 事件触发执行的 Hook 脚本。由这两个事件触发执行的
Hook 脚本将使用 *root* 用户运行并且不从 VDSM 进程中继承运行环境。

