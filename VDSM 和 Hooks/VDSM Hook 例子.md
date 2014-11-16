# VDSM Hook 例子

您必须确保不管从哪个来源安装到您的系统中的 Hook
脚本，都针对您的环境进行过全面的测试。

*目标：*.
此 Hook 脚本将根据 *hostusb* 自定义属性的值来使得虚拟机能够使用主机上的
USB 设备。如果该自定义选项的值未被设置，则不会执行任何操作。

> **Important**
>
> 使用此 Hook
> 要求必须把虚拟机固定在单独一台主机上运行，该虚拟机的迁移操作都会失败。

    hostusb=0x[\da-fA-F]{4}:0x[\da-fA-F]{4}(&0x[\da-fA-F]{4}:0x[\da-fA-F]{4})*


上面使用的正则表达式使得 *hostusb*
这个自定义属性能够接受一个或者多个由“:”分隔的两个四位十六进制数（例如
0x1234:0xbeef）的组合，如果是多个的话则它们之间由“&”分隔。其中每个组合表示一个主机上的
USB 设备，前面一个四位十六进制数表示厂商的 ID，后一个十六进制数表示产品
ID（例如刚才的例子，0x1234 表示厂商，0xbeef 表示产品）。

*脚本：*.
*/usr/libexec/vdsm/hooks/before\_vm\_start/50\_hostusb*


    #!/usr/bin/python

    import re
    import os
    import sys
    import grp
    import pwd
    import traceback

    import hooking

    '''
    host usb hook
    =============

              !!! Disclaimer !!!
    *******************************************
    The host side usb support wasn't thoroughly
    tests in kvm!
    *******************************************

    add hosts usb device/s to VM:

    <hostdev mode='subsystem' type='usb'>
        <source>
            <vendor id='0x1234'/>
            <product id='0xbeef'/>
        </source>
    </hostdev>

    syntax:
        hostusb=0x1234:0xbeef&0x2222:0xabaa
        i.e.
        hostusb=VendorId:ProductId (can add more then one with '&' separator)

    Note:
        The VM must be pinned to host and this hook will
        fail any migration attempt.
    '''

    HOOK_HOSTUSB_PATH = '/var/run/vdsm/hooks/hostusb-permissions'


    def log_dev_owner(devpath, user, group):
        entry = devpath + ":" + str(user) + ":" + str(group)

        if not os.path.isdir(os.path.dirname(HOOK_HOSTUSB_PATH)):
            os.mkdir(os.path.dirname(HOOK_HOSTUSB_PATH))

        if os.path.isfile(HOOK_HOSTUSB_PATH):
            f = file(HOOK_HOSTUSB_PATH, 'r')
            for line in f:
                if entry == line:
                    f.close()
                    return

        f = file(HOOK_HOSTUSB_PATH, 'a')
        f.writelines(entry)
        f.close()


    def chown(vendorid, productid):

        # remove the 0x from the vendor and product id
        devid = vendorid[2:] + ':' + productid[2:]
        command = ['lsusb', '-d', devid]
        retcode, out, err = hooking.execCmd(command, sudo=False, raw=True)
        if retcode != 0:
            sys.stderr.write('hostusb: cannot find usb device: %s\n' % devid)
            sys.exit(2)

        # find the device path:
        # /dev/bus/usb/xxx/xxx
        devpath = '/dev/bus/usb/' + out[4:7] + '/' + out[15:18]
        stat = os.stat(devpath)

        group = grp.getgrnam('qemu')
        gid = group.gr_gid
        user = pwd.getpwnam('qemu')
        uid = user.pw_uid

        # we don't use os.chown because we need sudo
        owner = str(uid) + ':' + str(gid)
        command = ['/bin/chown', owner, devpath]
        retcode, out, err = hooking.execCmd(command, sudo=True, raw=True)
        if retcode != 0:
            sys.stderr.write('hostusb: error chown %s to %s, err = %s\n' %
                             (devpath, owner, err))
            sys.exit(2)

        log_dev_owner(devpath, stat.st_uid, stat.st_gid)


    def create_usb_device(domxml, vendorid, productid):
        hostdev = domxml.createElement('hostdev')
        hostdev.setAttribute('mode', 'subsystem')
        hostdev.setAttribute('type', 'usb')

        source = domxml.createElement('source')
        hostdev.appendChild(source)

        vendor = domxml.createElement('vendor')
        vendor.setAttribute('id', vendorid)
        source.appendChild(vendor)

        product = domxml.createElement('product')
        product.setAttribute('id', productid)
        source.appendChild(product)

        return hostdev

    if 'hostusb' in os.environ:
        try:
            regex = re.compile('^0x[\d,A-F,a-f]{4}$')
            domxml = hooking.read_domxml()
            devices = domxml.getElementsByTagName('devices')[0]

            for usb in os.environ['hostusb'].split('&'):
                vendorid, productid = usb.split(':')
                if len(regex.findall(vendorid)) != 1 or \
                        len(regex.findall(productid)) != 1:
                    sys.stderr.write('hostusb: bad input, expected 0x0000 format '
                                     'for vendor and product id, input: %s:%s\n' %
                                     (vendorid, productid))
                    sys.exit(2)

                hostdev = create_usb_device(domxml, vendorid, productid)
                devices.appendChild(hostdev)
                chown(vendorid, productid)

            hooking.write_domxml(domxml)
        except:
            sys.stderr.write('hostusb: [unexpected error]: %s\n' %
                             traceback.format_exc())
            sys.exit(2)



