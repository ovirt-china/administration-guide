# 为虚拟机配置qxl驱动

*摘要*.
用户可以使用下面的任何一种步骤来配置 qxl 驱动

点击系统。

点击点击管理。

点击显示。

点击硬件。

点击视频卡配置。

选择 qxl，点击 确定。

重新登陆 X-Windows。

备份 /etc/X11/xorg.conf:

    # cp /etc/X11/xorg.conf /etc/X11/xorg.conf.$$.backup


改变/etc/X11/xorg.conf相关内容为以下:

    Section "Device"
    Identifier "Videocard0"
    Driver "qxl" Endsection


*结果*.
qxl 驱动已经配置好，现在可以使用了。
