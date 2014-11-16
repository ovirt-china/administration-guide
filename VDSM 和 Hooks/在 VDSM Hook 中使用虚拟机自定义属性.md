# 在 VDSM Hook 中使用虚拟机自定义属性

*前提需求：*

-   ?

-   ?

在*自定义属性*标签下为虚拟机设置的每个键值对都将在调用 Hook
脚本时被作为环境变量添加进运行环境中。虽然用以验证*自定义属性*标签下输入的值的正则表达式提供了部分保护功能，您还是必须确保您的脚本同样验证了这些值的输入与它们的预期值相匹配。

下面简短的 Python 例子检查了自定义属性 *key1*
是否存在。如果该自定义属性被设置则其值将被打印到标准错误输出中。如果该自定义属性未被设置，则不会进行任何操作。

    #!/usr/bin/python

    import os
    import sys

    if os.environ.has_key('key1'):
        sys.stderr.write('key1 value was : %s\n' % os.environ['key1'])
    else:
        sys.exit(0)


