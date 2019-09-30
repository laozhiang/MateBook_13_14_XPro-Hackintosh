# 多系统启动菜单
## 声明1：
1、本文记录试用grub启动win和mac的配置情况，在官方grub基础上增加了wimboot（来自于github上某个项目）模块，支持启动winpe的iso文件，不再需要制作winpe U盘<BR>

## 一、安装
将"启动带单.zip"解压后,把BootMenu目录拷贝硬盘EFI分区EFI目录下<BR>
试用easyUEFI然后增加硬盘启动项,并设为默认 \EFI\BootMenu\grubx64.efi

## 附1、系统启动背景知识
UEFI启动需要读取硬盘/U盘EFI分区的数据。EFI就是一个普通的FAT32分区，不一定是第一个分区，可以在硬盘的任意位置。<BR>

U盘、移动硬盘和硬盘的启动有所不同。
- U盘和移动硬盘: 启动时BIOS会直接查找EFI分区的EFI/BOOT/Bootx64.efi文件进行启动。
- 硬盘：一般系统安装会在BIOS中增加启动项。比如windows会增加一个启动项指向\EFI\Microsoft\Boot\bootmgfw.efi,ubuntu 启动项指向\EFI\ubuntu\shimx64.efi。只有在没有配置任何启动项时才会使用EFI/BOOT/BootX64.efi,所以硬盘的BOOTX64.efi基本没用


ubuntu下使用efibootmgr命令查看类似于
    ```
    >efibootmgr -v
    BootCurrent: 0001
    Timeout: 0 seconds
    BootOrder: 0001,0002,2001,2002,2003
    Boot0001* Windows Boot Manager	HD(1,GPT,8a6b4601-717c-481c-9ca5-9281f6f9914e,0x1000,0xe0000)/File(\EFI\Microsoft\Boot\bootmgfw.efi)WINDOWS.........x...B.C.D.O.B.J.E.C.T.=.{.9.d.e.a.8.6.2.c.-.5.c.d.d.-.4.e.7.0.-.a.c.c.1.-.f.3.2.b.3.4.4.d.4.7.9.5.}....................
    Boot0002* ubuntu	HD(1,GPT,8a6b4601-717c-481c-9ca5-9281f6f9914e,0x1000,0x100000)/File(\EFI\ubuntu\shimx64.efi)
    Boot2001* EFI USB Device	RC
    Boot2002* EFI DVD/CDROM	RC
    Boot2003* EFI Network	RC
    ```
## 附2、CLOVRE如何配置两套文件
CLOVER的启动过程是直接加载当前分区的EFI/CLOVER/config.plist文件。也就是分目录没用，所以一台机器想用两套配置，又不想每次启动都要操作几步选取配置文件的方法是，增加一个FAT32分区，大小够放下一个clover就行。拷贝CLOVE到新增EFI分区EFI目录,配置启动菜单，设定root分区为新增FAT32分区，加载相应clover。这样就可以做到两个启动配置了(可参考启动菜单配置文件中配置修改)


## 附3、linux添加硬盘启动项
- 查看Bios启动菜单
    ```
    efibootmgr
    ```
- 查看Bios启动菜单详细信息
    ```
    efibootmgr -v
    ```
- 添加启动项
  注意一下命令的两个参数，查看记住的分区信息，盘为/dev/nvme0n1；分区为/dev/nvme0n1p1
   - -d /dev/sda 这个是你盘的标识
   - -p 1 这个分区的序号，就是分区中P后面的数字
    ```
    sudo efibootmgr -c -w -L "BootMenu" -d dev/nvme0 -p 1 -l \\EFI\\BootMenu\\grubx64.efi
    ```
- 删除启动项目 0013为删除启动项的标号
    ```
    sudo efibootmgr -b 0013 -B
    ```
- 修改boot 顺序
    ```
    root@ubuntu:~# efibootmgr -o 0012,0010,0011,000F,000D,000C,000B   
    ```
