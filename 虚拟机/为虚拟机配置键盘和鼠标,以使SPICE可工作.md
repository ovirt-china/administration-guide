# 为虚拟机配置键盘和鼠标,以使SPICE可工作

*摘要*.
编辑 /etc/X11/xorg.conf，来启动 spice 的 tablet 设备。

确保 tablet 设备在系统中被识别出来。

    # /sbin/lsusb -v | grep 'QEMU USB Tablet'


如果没有任何输出的话，没必要配置 tablet 设备了。

备份 /etc/X11/xorg.conf:

    # cp /etc/X11/xorg.conf /etc/X11/xorg.conf.$$.backup


修改 /etc/X11/xorg.conf 的相关内容为:。

    Section "ServerLayout"
    Identifier Screen InputDevice InputDevice InputDevice EndSection
    "single head configuration" 0 "Screen0" 0 0
    "Keyboard0" "CoreKeyboard" "Tablet" "SendCoreEvents" "Mouse" "CorePointer"
    Section "InputDevice" Identifier "Mouse"
    Driver #Option #Option EndSection
    "void"
    "Device" "/dev/input/mice" "Emulate3Buttons" "yes"
    Section "InputDevice"
    Identifier "Tablet"
    Driver "evdev"
    Option "Device" "/dev/input/event2" Option "CorePointer" "true"
    EndSection


重新登陆 X-Windows。

*结果*.
已经在虚拟机中启用了 tablet 设备了。
