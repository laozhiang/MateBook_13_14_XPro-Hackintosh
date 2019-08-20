# Matebook X Pro 2019 黑苹果教程
## 声明1：
1、目前只支持 Mac OSX Majave 10.14.5，只支持10.14.5，只支持10.14.5<BR>
2、想折腾的自己搞，不想自己折腾的还是算了吧，各种坑巨多<BR>
3、没有装过苹果的机友建议一步一步按照文档来，别做过多动作，想太多不一定是好事<BR>
4、初次安装的朋友，注意备份数据，也可以先用移动硬盘试装<BR>
5、个人机器由于更换了主板，DSDT与零售版不一致，部分功能为网友测试

## 声明2:
个人理解黑苹果重在稳定，所以不会盲目的更新版本，不追新。每年更新一个OSX的大版本或重大更新，其余一律不跟风，也不要提更新的issue，有兴趣的机友可以自己更新。

## 文档说明：
1、记录Matebook X Pro 2019版黑苹果安装过程<BR>
2、本文仅记录黑苹果过程，不涉及多系统安装。多系统启动参见<BR>
3、问题交流请到QQ群：812158410
≈
## 一、机型配置信息
| 项目 | 详细参数|
| :--: | :-------------------- |
| 型号 | Matebook X Pro 2019 i5 集显版，经其他机友确认，支持15/17独显   |
| CPU  | i5 8265u |
|内存| DDR3L 8G|
| 显卡 | UHD620|
| 硬盘 | 该机型已知有两种硬盘<BR>西数硬盘SN720不存在问题<BR>三星PM981不支持黑苹果(970 EVO PlUS一样不支持),需要使用外置硬盘或更换硬盘|
| 声卡 | Realtek ALC256 |
|LCD| 该机型已知两种显示器，配置文件中内建显示器不同，所以有两套不同的配置文件，需要自行选择<BR>一种为TLX1388<BR>一种为<BR>
|BIOS|请确认升级到1.15|
| | |

## 二、成果
| 项目 | 成果|
| :--: | :-------------------- |
| 版本 | Mac OSX Majave 10.14.5（目前仅支持，其他版本需要找到相应补丁） |
| 电源   | OK |
| 电池电量 | OK |
| 显示   | 内屏OK<BR>DP外接屏OK<BR>HDMI外接屏无网友测试OK<BR>外接4K不稳定，开启启动后偶尔黑屏，需要合盖开盖后正常，因此有两套配置文件，根据个人需要选择|
| 亮度 | OK |
| 键盘调整亮度| OK，FN+F1/FN+F2调整，显示小太阳 |
| 自动调整亮度| NOK|
| 声音   | 半OK，目前外放和micOK，耳麦存在问题|
| 键盘调音量| OK |
| 触摸屏 | OK |
| 触摸板 | OK |
| WIFI  | 全球无解，建议采用外接USB WiFi 适配器，需要确认是否支持MAC。需要占用USB端口|
| 蓝牙   | 方式1、曲线救国，安装虚拟机，使用库上蓝牙启动包，驱动蓝牙<BR>方式2、采用USB蓝牙适配器，BIOS中关闭机器自带蓝牙，这种方式需要占用USB端口，所以需要扩展坞|
| 摄像头 | OK |
|睡眠唤醒 | OK |
|合盖睡眠 | OK<BR> 两种情况<BR>1、外接电源同时外接显示器时，切换为台式机模式，外屏不关<BR>2、非同时外接电源和显示器时机器直接睡眠|
|开盖唤醒 | OK |
| 睿频 | OK|
|  | |
## 三、问题记录
- 启动：偶尔启动不成功，建议启动不关闭啰嗦模式
- 登录界面偶尔黑屏：如果出现该情况，合上笔记本，等几秒，再打开看看是否OK。
- 声卡：目前没有搞定驱动，外放和MIC可用，耳麦有问题，详情见安装后处理
- 蓝牙：两种支持方式，参见成果描述
- 独显：不支持
- 指纹： 不支持
## 四、安装需求
- USB Hub或扩展坞(必须)-该机型仅有1个USB接口，安装需要两个USB设备，U盘和USB鼠标
- U盘 8G以上（必须）
- USB鼠标（必须，非蓝牙鼠标）有线无线均可，安装过程中触摸板不可用
- WinPE U盘（非必须），出现问题需要WinPE启动解决，安装后需要通过windows下的easyUEFI添加启动项，Linux机友Live系统U盘也可
- 如安装到移动硬盘，请外接电源（已经出现几例未外接电源启动不成功的），安装过程中出现突然重启或错误可以尝试换一下移动硬盘接入端口，建议接雷电口  
个人建议：多用ubuntu 18.4做一个安装盘，其中包含liveCD，linux下一些操作比widows要方面很多。
精通多重启动的用户可以一个U盘包含winpe，和linuxCD
## 五、小白版安装过程
### 1、软件下载
| 软件 | 是否必须 | 用途 | 下载地址 |
| :--: | :--: | :--: | :-------------------- |
| MoJave镜像 | 无MAC机友必须 | - | 仅为推荐地址，相同版本的其他下载也可以，不保证好用，改版本是经过机友测试的<BR> https://blog.daliansky.net/macOS-Mojave-10.14.5-18F132-official-version-with-Clover-4928-original-image.html |
| DiskGenius | 非必须 |制作winPE，调整硬盘分区|http://www.diskgenius.com |
| EasyUEFI | Windows机友必须；<BR>Linux使用efibootmgr即可| 确认使用OK后，增加硬盘启动项 |未找到官方下载地址|
|Github安装包 | 必须 | 黑苹果启动|https://github.com/laozhiang/MateBook_X_Pro_2019-Hackintosh<BR> 下载方法：|
|  | |
### 2、制作安装盘
#### 无MAC机友----网上找制作说明
本来写了这部分说明，发现大家都是在下载点看说明，因此删掉<BR>。请注意，只看下载点说明的镜像制作部分，安装部分做好别看，和本文相似，但是非专用说明，有坑。<BR>
使用工具将DMG文件写到U盘后，需要以下处理
- step1: 将在github上下载的文件全部拷贝的安装盘上(安装后，在MAC系统中添加驱动过程需要)，建议新建一个目录存放(做安装U盘的工具应支持，使用transMAC软件可以操作，或者更简单放到另外一个FAT32格式U盘上备用)
- step2: 删除U盘EFI分区上EFI目录(镜像中自带EFI为通用配置，不适用，启动不成功)<BR>
- step3: 解压缩EFI_for_Install_USB.zip<BR>
- step4: 打开DiskGenius,左侧选择U盘，选装EFI分区，将EFI_for_Install_USB解压缩后目录拷贝到EFI分区，并重命名为EFI  
<B>结束后EFI分区内目录格式，请注意核对</B>

	```
	EFI
	  |----BOOT
	  |      |-BOOTX63.efi
	  |----CLOVER
	  |      |-......
	  |      |-......
	```
  #### 有MAC机友
- Step1： 通过AppStore下载OSX安装包（现在下不了了，官方只支持最新版下载，找以前的备份吧）
- Step2：打开 “应用程序 → 实用工具 → 磁盘工具”，将U盘「抹掉」(格式化) 成「Mac OS X 扩展（日志式）」格式、GUID 分区图，并将 U 盘命名为「Install macOS Mojave」。注意：这个盘符名称必须与后面的命令里的名称一致，需要认真看清楚，很多新手容易出错在这里)
- Step3：打开 “应用程序→实用工具→终端”，将下面的一段命令复制并粘贴进去：

 	如要U盘命名为「Mojave」，命令中 「/Volumes/Install\ macOS\ Mojave」需要改为「/Volumes/Mojave」

		```
		sudo /Applications/Install\ macOS\ Mojave.app/Contents/Resources/createinstallmedia --volume /Volumes/Install\ macOS\ Mojave /Applications/Install\ macOS\ Mojave.app --nointeraction
		```
- Step4: 回车并执行上方命令，这时会提示让你输入管理员密码，便会开始制作过程
- Step5: 请耐心等待，时间较长，等待命令执行结束。
- Step6: 把github上下载文件拷贝到U盘上，建议新建目录，安装后完善用
- Step7: 将github下载文件中EFI_for_Install_USB.zip解压缩后拷贝到EFI分区，并重命名为EFI<BR>
不会挂在EFI分区机友，可是使用下载文件中tools目录下"Clover Configurator.zip“，打开软件，左侧选择“挂载分区”，右侧下部选中U盘的EFI，点击挂载分区，此时弹出窗口输入密码，确认即可，在桌面找到EFI盘符可进入
<B>结束后EFI分区内目录格式，请注意核对</B>

	```
	EFI
	  |----BOOT
	  |      |-BOOTX63.efi
	  |----CLOVER
	  |      |-......
	  |      |-......
	```
### 3、现在开始动硬盘了，请一定要备份好数据，可能整个盘数据全丢，尤其是新黑苹果玩家
### 4、调整硬盘分区
这部分出问题最多，很多人又想留着原系统和一键还原。只能自己操作<BR>
强烈建议，这一步使用DiskGenius制作一个WINPE，在winPE下操作<BR>
强烈建议，windows机友准备一个包含easyUEFI的winpe U盘，如果安装过程中，一不小心抹除全盘，需要在winPE下增加硬盘启动项

硬盘和移动硬盘同样适用
- EFI分区要保证大于200M<BR>
- 使用DiskGenius分一个分区，格式为hpfs+

关于分区的其他建议：
  建议多分一个FAT32的分区，32M足矣，1）用来保存以下你认为完美的配置，备份EFI分区，2）避免Windows更新导致启动文件丢失，3）如果你需要多套配置（外接4K和非外接4K启动两个启动项）。<BR>

补充知识：BIOS启动U盘、移动硬盘和硬盘有所不同
- U盘、移动硬盘启动：BIOS查找盘上EFI分区的EFI/BOOT/BOOTX64.efi,进行启动<BR>
- 硬盘启动：硬盘是根据注册到BIOS中的启动项进行启动，BIOS启动项增删改查方式，window有命令BCDEDIT，或者用工具EasyUEFI，linux使用efibootmgr命令<BR>

### 5、开始安装
- Step1：开机直接按F2，进入BIOS设置界面
- Step2：关闭相关硬盘启动项。理由：安装过程中全部使用U盘启动，每次开机按F12选择启动菜单来不及
- Step3：关闭安全启动
- Step4：使用PM981硬盘的机友，安装到移动硬盘上，请关闭设置界面下半部分的HDD设备。理由：PM981会造成不定时重启，增加安装难度
- Step5：F10保存，重启
- step6、按F12选择U盘启动
- step7、进入安装过程<BR>
这部分我就不写了，这部分网上教程很多。<BR>
容易出现问题：<BR>
1）无法选择安装盘，一般是分区抹盘失败/EFI小于200M<BR>2) 抹盘失败基本是分区没搞好

### 5、安装后处理
#### 添加驱动
- Step1:将github下载patch目录下AppleIntelCFLGraphicsFramebuffer.kext.zip解压缩
- Step2:打开“访达”窗口，菜单选择“前往”->“前往文件夹”；弹出窗口，输入“/System/Library/Extensions",前往，找到AppleIntelCFLGraphicsFramebuffer.kext，删除
- step3:将AppleIntelCFLGraphicsFramebuffer.kext.zip解压得到文件拷贝到“/System/Library/Extensions"
- step4:找到github下载tools目录下Kext Utility2.6.6.zip解压并执行进行重建驱动缓存，需要输入用户密码。时间教程请耐心等待，只到下方“Quit”按钮可用
- Step5:打开U盘EFI分区；不会挂载EFI分区机友，可是使用github下载文件中tools目录下“Clover Configurator.zip"，打开软件，左侧选择“挂载分区”，右侧下部选中U盘的EFI分区，点击挂载分区，此时弹出窗口输入密码，确认即可，在桌面找到EFI盘符可进入
- step6:进入EFI分区，EFI目录将Clover目录改名为“CloverInstall”
- step7:把github下载的CLOVER复制到U盘EFI分区EFI目录下
- step8:挂载硬盘EFI分区，方法同上
- step9:把github下载的EFI_MateBookXpro2019.zip解压缩，并将其中CLOVER复制到EFI分区EFI目录下
- step10:重启

	此时效果 显卡，电源、触摸板、声卡等基本OK，蓝牙不可用。
#### 处理蓝牙
- Step1:安装VMware fusion，软件包激活码自行查找
- Step2:解压蓝牙启动工具.zip,将解压后文件中“蓝牙启动.zip”解压缩到当前用户目录，虚拟机 目录下
- Step3:双击执行蓝牙脚本目录的 install.command
- Step4:重新启动

	安装脚本已经安装开机启动功能，开机自动启动虚拟机驱动蓝牙<BR>安装脚本会在桌面创建"蓝牙启动.command",蓝牙不能连接时，可以双击脚本重新驱动蓝牙，<BR>
#### 处理启动啰嗦模式界面
  打开EFI分区EFI/CLOVER/config.plist
  找到
 ```
  <key>Boot</key>
	<dict>
		<key>Arguments</key>
		<string>-v -cdfon -igfxmlr dart=0</string>
		<key>Debug</key>
		<false/>
	</dict>
  ```
  <B>删除-v即可</B>
## 六、安装完成

## 七、安装用Clover制作（以下为进阶材料，想了解CLOVER具体是如何配置出来的朋友参考，目前尚不完整）
### 软件及版本
| 软件 | 版本 | 下载地址 |
| :--: | :--: |:-------------------- |
| CLOVER | v2.5k_r5033 |https://sourceforge.net/projects/cloverefiboot/ 建议下载ISO版本|
| VoodooPS2Controller.kext |2018-1008 | https://bitbucket.org/RehabMan/os-x-voodoo-ps2-controller |
| Lilu.kext | 1.3.7 | https://github.com/acidanthera/Lilu |
|  | |
### 制作工具
### 制作过程
- 解压CloverISO-5033.tar.lzma为CloverISO-5033.iso（linux下可以直接解压，其他系统未知，您有其他系统方法通知作者更新说明）
- 将EFI目录复制到您的工作目录
- 删除EFI/CLOVER/doc目录
- 进入EFI/CLOVER/dirvers目录，删除BIOS目录，删除off目录
- 进入EFI/CLOVER/dirvers/UEFI目录，删除AudioDex.efi、Fat.efi
- 解压Liu，把Lilu.kext放到EFI/CLOVER/kexts/Other/
- 解压RehabMan-Voodoo-2018-1008；把Release目录下VoodooPS2Controller.kext拷贝到EFI/CLOVER/kexts/Other/目录下；点击VoodooPS2Controller.kext，右键显示包内容，进入Contents/Plugins目录，删除VoodooPS2Mouse.kext、VoodooPS2Trackpad.kext
- 在themes添加您喜爱的theme
- 开始修改config.plist（后续再写）

## 七、Clover修改过程

| 软件 | 版本 |下载地址 |
| :--: |:--: |:-------------------- |
| CLOVER | v2.5k_r5033 |https://sourceforge.net/projects/cloverefiboot/|
| VirtualSMC | 1.0.6 | https://github.com/acidanthera/VirtualSMC |
| VoodooPS2Controller.kext |2018-1008 | https://bitbucket.org/RehabMan/os-x-voodoo-ps2-controller |
| Lilu.kext | 1.3.7 | https://github.com/acidanthera/Lilu |
| WhateverGreen.kext |1.3.0 | https://github.com/acidanthera/WhateverGreen |
| AptioMemoryFix.efi | AptioFixPkg R27 |https://github.com/acidanthera/AptioFixPkg|
| AppleALC | 1.3.9 |https://github.com/acidanthera/AppleALC|
|  | |
| VoodooI2C.kext<br>VoodooI2CHID.kext | 2.2 | https://github.com/alexandred/VoodooI2C |
|  | |
| SSDT-XOSI.dsl<br>SSDT-PNLFCFL | |https://github.com/RehabMan/OS-X-Clover-Laptop-Config |
|  | |

### 制作过程
#### 1、基础制作
- 解压CloverISO-5033.tar.lzma为CloverISO-5033.iso（linux下可以直接解压，其他系统未知，您有其他系统方法通知作者更新说明）
- 将EFI目录复制到您的工作目录
- 删除EFI/CLOVER/doc目录
- 进入EFI/CLOVER/dirvers目录，删除BIOS目录，删除off目录
- 进入EFI/CLOVER/dirvers/UEFI目录，删除Fat.efi（可以不删这个文件）
- 替换SMChelper为VirtualSMC
  - 进入EFI/CLOVER/dirvers/UEFI目录，删除SMCHelper.efi
  - 解压VirtualSMC，将Drivers/VirtualSmc.efi拷贝到EFI/CLOVER/dirvers/UEF/
  - 进入EFI/CLOVER/kexts/Other目录，删除FakeSMC.kext
  - 将VirtualSMC解压后Kexts/VirtualSMC.kext拷贝到EFI/CLOVER/kexts/Other/
- Drivers
- 替换OsxAptioFix3Drv.efi为AptioMemoryFix.efi
  - 进入EFI/CLOVER/dirvers/UEFI目录，删除OsxAptioFix3Drv.efi
  - 解压AptioFixPkg，将AptioMemoryFix.efi拷贝到EFI/CLOVER/dirvers/UEFI /
- 解压Liu，把Lilu.kext放到EFI/CLOVER/kexts/Other/
- 解压WhateverGreenLiu，把WhateverGreen.kext放到EFI/CLOVER/Kexts/Other/
- 解压RehabMan-Voodoo-2018-1008；把Release目录下VoodooPS2Controller.kext拷贝到EFI/CLOVER/Kexts/Other目录下；点击VoodooPS2Controller.kext，右键显示包内容，进入Contents/Plugins目录，删除VoodooPS2Mouse.kext、VoodooPS2Trackpad.kext
- 在themes添加您喜爱的theme
- 开始修改config.plist（后续再写）
  ```
  <key>Fixes</key>
		<dict>
			<key>AddDTGP</key>
		<true/>
		</dict>
	```
  ```
	<key>Patches</key>
	change HWEC to EC
  change ECAV=One to ECTK=zero(本机特有改动，具体看USB版描述，最后这个修改会删除)
  change _QA8 to XQA8（驱动电池后可删除）
  change _QA9 to XQA9（驱动电池后可删除)
  change Method(_Q0A,0,N) to XQ0A
  change Method(_Q0B,0,N) to XQ0B
  Comment: Fix AsRock Z390 BIOS DSDT Device(RTC) bug
  change GFX0 to IGPU
  change HDAS to HDEF
  change HECI to IMEI
  change OSID to IDOS
  change _OSI to XOSI
  change  _CRS to XCRS in TPD0
   ```
  ```
		<key>KernelToPatch</key>
		<array>
			<dict>
				<key>Comment</key>
				<string>MSR 0xE2 _xcpm_idle instant reboot(c) Pike R. Alpha</string>
				<key>Disabled</key>
				<false/>
				<key>Find</key>
				<data>
				ILniAAAADzA=
				</data>
				<key>Replace</key>
				<data>
				ILniAAAAkJA=
				</data>
			</dict>
		</array>
  ```
  ```
 		<key>KextsToPatch</key>
		<array>
			<dict>
				<key>Comment</key>
				<string>Prevent Apple I2C kexts from attaching to I2C controllers, credit CoolStar</string>
				<key>Disabled</key>
				<false/>
				<key>Find</key>
				<data>
				SU9LaXQ=
				</data>
				<key>InfoPlistPatch</key>
				<true/>
				<key>Name</key>
				<string>com.apple.driver.AppleIntelLpssI2C</string>
				<key>Replace</key>
				<data>
				SU9LaXM=
				</data>
			</dict>
			<dict>
				<key>Comment</key>
				<string>Prevent Apple I2C kexts from attaching to I2C controllers, credit CoolStar</string>
				<key>Disabled</key>
				<false/>
				<key>Find</key>
				<data>
				SU9LaXQ=
				</data>
				<key>InfoPlistPatch</key>
				<true/>
				<key>Name</key>
				<string>com.apple.driver.AppleIntelLpssI2CController</string>
				<key>Replace</key>
				<data>
				SU9LaXM=
				</data>
			</dict>
		</array>
	</dict>
  ```
以上修改后，已经可以启动机器，但是设备基本未驱动，尤其是显卡，导致系统卡<BR>
注：很多人建议将VBoxHfs.HFSPlus.efi,但是该文件未找到出处，暂时不替换（知道出处可以通知我）
#### 2、驱动显卡
驱动显卡是一个比较麻烦的事情，
- 首先、笔记本的DMT pre allocate在Bios里设置为32M，并且为隐藏设置，不能修改，这对于3K屏来说不可接受，apple在驱动会根据苹果的设定来做，此处内存不够，导致无法启动
- 其次、matebook X pro 2019的CPU不是苹果默认支持的，需要仿冒显卡ID
- 第三、显卡输出，输出端口类型需要考虑外接屏类型<BR>
  
修改步骤,每一个都够写很多的，简单写一点<BR>
1、仿冒显卡ID根据建议选择3E9B0000<BR>
通过tools下面Hackintool软件生成，仿冒ID3E9B0000，
```
		<key>Properties</key>
		<dict>
			<key>PciRoot(0x0)/Pci(0x2,0x0)</key>
			<dict>
				<key>AAPL,ig-platform-id</key>
				<data>
				AACbPg==
				</data>
				<key>AAPL,slot-name</key>
				<string>Internal</string>
				<key>device-id</key>
				<data>
				mz4AAA==
				</data>
				<key>device_type</key>
				<string>VGA compatible controller</string>
				<key>enable-hdmi20</key>
				<data>
				AQAAAA==
				</data>
				<key>framebuffer-con0-enable</key>
				<data>
				AQAAAA==
				</data>
				<key>framebuffer-con0-pipe</key>
				<data>
				EgAAAA==
				</data>
				<key>framebuffer-con1-enable</key>
				<data>
				AQAAAA==
				</data>
				<key>framebuffer-con1-pipe</key>
				<data>
				EgAAAA==
				</data>
				<key>framebuffer-con2-enable</key>
				<data>
				AQAAAA==
				</data>
				<key>framebuffer-con2-pipe</key>
				<data>
				EgAAAA==
				</data>
				<key>framebuffer-fbmem</key>
				<data>
				AACQAA==
				</data>
				<key>framebuffer-patch-enable</key>
				<data>
				AQAAAA==
				</data>
				<key>framebuffer-stolenmem</key>
				<data>
				AAAABA==
				</data>
				<key>framebuffer-unifiedmem</key>
				<data>
				AAAAgA==
				</data>
				<key>model</key>
				<string>UHD Graphics 620 (Mobile)</string>
			</dict>
		</dict>
```
2、针对DVMT打补丁<BR>
通过tools下面Hex Fiend修改
```
Coffelake 8th:AppleIntelCFLGraphicsFramebuffer.kext
Kext: com.apple.driver.AppleIntelCFLGraphicsFramebuffer.kext
Find: 764648FF 052B3B09
Repl: EB4648FF 052B3B09
Comment: Disable minStolenSize less or equal fStolenMemorySize assertion, 10.14.5  (based on Austere.J patch by Len)
```
3、生成相应记性SMBios "MacBookPro15,2"
通过tools下面Clover Configurator生成SMbios，机型选择“MacBookPro15,2”
另存为一个配置文件，截取其中
  ```
	<key>SMBIOS</key>
	<dict>
       ......
       ......
	</dict>
  ```
  写入config.plist
3、内置显示器<BR>
提取EDID
写入显卡属性中
```
				<key>AAPL00,override-no-connect</key>
				<data>AP///////wAoiSpCAAAAAAAbAQSQHRR4A95Qo1RMmSYPUFQAAAABAQEBAQEBAQEBAQEBAQEBt5i4oLDQPnAIIAgMJcQQAAAat5i4oLDQQXIIIAgMJcQQAAAaAAAA/gBKREkgICAgICAgICAgAAAA/gBMUE0xMzlNNDIyQSAgAE4=</data>
```
#### 3、驱动声卡
  - 解压AppleALC，将AppleALC.kext拷贝到EFI/CLOVER/kexts/Other/
  - config.plist文件，在Devices/Properties下添加配置项,注入声卡
```
			<key>PciRoot(0x0)/Pci(0x1f,0x3)</key>
			<dict>
				<key>AAPL,slot-name</key>
				<string>PCI-Express</string>
				<key>hda-gfx</key>
				<string>onboard-1</string>
				<key>hda-idle-support</key>
				<string>1</string>
				<key>layout-id</key>
				<integer>57</integer>
				<key>model</key>
				<string>Intel Sunrise Point-LP HD Audio</string>
			</dict>
```
#### 4、驱动触摸板
  - 解压VoodooI2C，将VoodooI2C.kext、VoodooI2CHID.kext拷贝到EFI/CLOVER/kexts/Other/
目前触摸板需要大力按才产生点击，并且由于没有驱动电源，无法打开触摸板控制板进行设置<BR>
采用命令行开启触摸板轻触为点击<BR>
因为有sudo，建议一下命令逐个执行
```
defaults write com.apple.AppleMultitouchTrackpad Clicking -bool true
sudo defaults write com.apple.driver.AppleBluetoothMultitouch.trackpad Clicking -bool true
sudo defaults -currentHost write NSGlobalDomain com.apple.mouse.tapBehavior -int 1
sudo defaults write NSGlobalDomain com.apple.mouse.tapBehavior -int 1
```
#### 5、驱动电源
- config.plist文件，将AC0改名为ADP1

#### 6、驱动电池
问题说明：19版的电池信息在embeddedConteol Region里面。在这个里面的数据需要操作系统初始化
苹果系统只初始化8位的数据，16位和32位不处理，在读取相应数据是读不出导致ECRD函数返回位初始化错误，这也是为什么前面要修改_QA8位XQA8。
这就让我们必须把这一段数据里定义的大于8位的数据都改成8位，16位改成2个8位数据，32位改成4个8位数据
在向苹果操作系统返回数据是，还需要把拆开的数据拼接起来，也就是把拆出来的两个8位数据拼接位一个16位数据返回，幸好，19版的BIOS只有8位和16位，拆解比较简单

```
B0ST,拆成两位
//B0ST,   16, 
BST1,   8, 
BST2,   8, 
读取B0FC的地方改为
//Store (ECRD (RefOf (B0ST)), Local0)
 Store (B1B2(ECRD (RefOf (BST1)),ECRD (RefOf (BST2))), Local0)	
```

大部分位读取，但是光传感器部分有写操作，只能一次写改成两次写，写前8位，然后在写后8位
```	
CALS,拆成两位
//CALS,   16, 
CAL1,   8, 
CAL2,   8, 
写CALS的地方拆成两句
//ECWT (Local0, RefOf (CALS))
ECWT (Local0, RefOf (CAL1))
ECWT (ShiftRight(Local0,8), RefOf (CAL2))
```
把embeddedConteol Region中定义的数据凡是有读写擦操作的拆完，没有读写的可以不拆
这样就可以删除config.plist中的
  
  change _QA8 to XQA8（驱动电池后可删除）
  change _QA9 to XQA9（驱动电池后可删除)
将修改后的DSDT.aml放到EFI/CLOVER/ACPI/patch目录下
添加电池驱动，点击VirtualSMC.kext，右键显示包内容，进入Contents新建Plugins目录，将解压VirtualSMC目录中的SMCBatteryManager.kext、SMCLightSensor.kext、SMCProcessor.kext、SMCSuperIO.kext拷贝到Plugins目录
电池OK了，触控板的控制面板也可以显示了
#### 7、显卡亮度调节
使用isal编译SSDT-PNLFCFL，生成SSDT-PNLFCFL.aml,放到EFI/CLOVER/ACPI/patch目录下
此时存在问题，开机不显示登陆chu窗口，需要开合一次笔记本，修改DSDT的亮度调节按钮可解决，原理未知
```
        Method (_Q0A, 0, NotSerialized)  // _Qxx: EC Query
        {
//            If (CondRefOf (HBRT))
//            {
//                HBRT (0x04)
//            }
//
//            If (And (0x04, DSEN))
//            {
//                BRTN (0x87)
//            }
//            Else
//            {
//                Store (^^^GFX0.CBLV, Local0)
//                And (Add (Local0, One), 0xFE, Local0)
//                If (LGreaterEqual (Local0, 0x0A))
//                {
//                    Subtract (Local0, 0x0A, Local0)
//                }
//
//                Store (Local0, BRTL)
//                ^^^GFX0.AINT (One, Local0)
//            }
			Notify(\_SB.PCI0.LPCB.PS2K, 0x0405)
            ADBG ("FN+F1")
        }

        Method (_Q0B, 0, NotSerialized)  // _Qxx: EC Query
        {
//            If (CondRefOf (HBRT))
//            {
//                HBRT (0x03)
//            }
//
//            If (And (0x04, DSEN))
//            {
//                BRTN (0x86)
//            }
//            Else
//            {
//                Store (^^^GFX0.CBLV, Local0)
//                And (Add (Local0, One), 0xFE, Local0)
//                If (LLessEqual (Local0, 0x5A))
//                {
//                    Add (Local0, 0x0A, Local0)
//                }
//
//                Store (Local0, BRTL)
//                ^^^GFX0.AINT (One, Local0)
//            }
            Notify(\_SB.PCI0.LPCB.PS2K, 0x0406)
            ADBG ("FN+F2")
        }
```
将修改后的DSDT.aml放到EFI/CLOVER/ACPI/patch目录下

#### 6、既然DSDT都改了，那就多改一点
1）去除config.plist中补丁change ECAV=One to ECTK=zero
```
                If (ECTK)
                {
//                    If (LGreaterEqual (_REV, 0x02))
//                    {
//                        Store (One, ECAV)
//                    }

                    Store (Zero, ECTK)
                }
```
删除config中的
