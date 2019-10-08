# Matebook X Pro 2019 黑苹果教程
## 已经支持Catalina 10.15， QQ群（777324370）内测试中，可以加群去用，预计10日上传
## 声明1：
1、目前只支持 Mac OSX Majave 10.14.5，只支持10.14.5，只支持10.14.5<BR>
2、没有所谓的完美，真想完美请买白果，想折腾的自己搞，不想自己折腾的还是算了吧，各种坑巨多<BR>
3、没有装过苹果的机友建议一步一步按照文档来，别做过多动作，想太多不一定是好事<BR>
4、初次安装的朋友，注意备份数据，也可以先用移动硬盘试装<BR>

## 声明2:
个人理解黑苹果重在稳定，所以不会盲目的更新版本，不追新。每年更新一个OSX的大版本或重大更新，其余一律不跟风，也不要提更新的issue，有兴趣的机友可以根据后面的说明自己更新。

## 文档说明：
1、记录Matebook X Pro 2019版黑苹果安装过程<BR>
2、本文仅记录黑苹果过程，不涉及多系统安装<BR>
3、问题交流请到QQ群：777324370

## 一、机型配置信息
| 项目 | 详细参数|
| :--: | :-------------------- |
| 型号 | Matebook X Pro 2019 i5 集显版，经其他机友确认，支持15/17独显   |
| CPU  | i5 8265u |
|内存| DDR3L 8G|
| 显卡 | UHD620|
| 硬盘 | 该机型已知有两种硬盘<BR>西数硬盘SN720不存在问题<BR>三星PM981不支持黑苹果(970 EVO PlUS一样不支持),需要使用外置硬盘或更换硬盘|
| 声卡 | Realtek ALC256 |
|LCD| 该机型已知两种显示器，<BR>一种为TLX1388<BR>一种为JDI<BR> |
|BIOS|请确认升级到1.15 |
| | |

## 二、成果
| 项目 | 成果|
| :--: | :-------------------- |
| 版本 | Mac OSX Majave 10.14.5 |
| 电源   | OK |
| 电池电量 | OK |
| 显示   | 内屏OK<BR>DP外接屏OK<BR>HDMI外接屏OK<BR>开启启动后偶尔黑屏，需要合盖开盖或按两次定制键F7可恢复正常<BR>由于bios预分配显存默认配置为32M,外接4K是需要修改bios隐藏配置将预分配显存修改为64M(有操作指导).因此产生两套配置DVMT32M和DVMT64M,默认为DVMT32M|
| 亮度   | OK |
| 键盘调整亮度| OK，FN+F1/FN+F2调整，显示小太阳 |
| 自动调整亮度| NOK|
| 声音   | 半OK，目前外放和micOK，耳麦存在问题|
| 键盘调音量| OK |
| 触摸屏 | OK |
| 触摸板 | OK |
| WIFI  | 全球无解，建议采用外接USB WiFi 适配器，需要确认是否支持MAC。需要占用USB端口(有指导说明)|
| 蓝牙  | 方式1、曲线救国，安装虚拟机，使用库上蓝牙启动包，驱动蓝牙<BR>方式2、采用USB蓝牙适配器，BIOS中关闭机器自带蓝牙，这种方式需要占用USB端口，所以需要扩展坞|
| 摄像头 | OK |
| 雷电 | NOK |
|睡眠/唤醒| OK |
|合盖睡眠| OK<BR> 两种情况<BR>1、外接电源同时外接显示器时，切换为台式机模式，外屏不关<BR>2、非同时外接电源和显示器时机器直接睡眠|
|开盖唤醒| OK |
| 睿频  | OK|
| 键盘处理 | Windows=Command<BR>Alt=options<BR> F1=亮度降低 <BR>F2=亮度增加<BR>F3=键盘灯<BR>F4=静音(无效)<BR>F5=音量减小<BR>F6=音量增加<BR>F7=开关内屏,应对开机黑屏或者开关显示器<BR>F8=F18,可以通过Karabiner软件转换为Command+F1,外接屏幕是转换扩展或镜像显示模式<BR>F9=建议F19通过设置键盘快捷方式,设置为重启蓝牙<BR>F10=启停止触摸板,<BR>F11=Prtsc/F13;通过设置键盘快捷方式实现截屏<BR>F12/Ins=电源键|
|      | |
## 三、问题记录
- 启动：偶尔启动不成功，重启之
- 登录界面偶尔黑屏：如果出现该情况合上笔记本等几秒再打开,或者按F7键,注意下方Fn键状态,看看是否OK。
- 声卡：已经申请提交代码,用耳机有些问题，来自耳机接口为二合一接口，芯片并没有设定外接MIC的端口，使用了虚拟端口。
- 蓝牙：两种支持方式，参见成果描述
- 独显：不支持
- 指纹：不支持
- 自动调整亮度: 不支持
- 雷电3: 不支持
## 四、安装需求
- USB Hub或扩展坞(必须)-该机型仅有1个USB接口，安装需要两个USB设备，U盘和USB鼠标
- U盘 8G以上（必须）
- USB鼠标（必须，非蓝牙鼠标）有线无线均可，安装过程中触摸板不可用
  ### 其他建议准备
- WinPE U盘（非必须），出现问题需要WinPE启动解决，安装后需要通过windows下的easyUEFI添加启动项，Linux机友Live系统U盘也可
- 如安装到移动硬盘，请外接电源（已经出现几例未外接电源启动不成功的），安装过程中出现突然重启或错误可以尝试换一下移动硬盘接入端口

## 五、小白版安装过程
### 1、软件下载
| 软件 | 是否必须 | 用途 | 下载地址 |
| :--: | :--: | :--: | :-------------------- |
| MoJave镜像 | 无MAC机友必须 | - | 仅为推荐地址，相同版本的其他下载也可以，不保证好用，该版本是经过机友测试的<BR> https://blog.daliansky.net/macOS-Mojave-10.14.5-18F132-official-version-with-Clover-4928-original-image.html |
| DiskGenius | 非必须 |制作winPE，调整硬盘分区|http://www.diskgenius.com |
| EasyUEFI | Windows机友必须；<BR>Linux使用efibootmgr即可| 确认使用OK后，增加硬盘启动项 |未找到官方下载地址|
|Github安装包 | 必须 | 黑苹果启动|https://github.com/laozhiang/MateBook_X_Pro_2019-Hackintosh/install 目录下文件<BR> 仅下载该目录下所有文件即可 |
|  | |
### 2、制作安装盘
#### 无MAC机友----网上找制作说明
本来写了这部分说明，发现大家都是在下载点看说明，因此删掉<BR>。请注意，只看下载点说明的镜像制作部分，安装部分做好别看，和本文相似，但是非专用说明，有坑。<BR>
使用工具将DMG文件写到U盘后，需要以下处理
- step1: 删除U盘EFI分区上EFI目录(镜像中自带EFI为通用配置，不适用，启动不成功)<BR>
- step2: 解压缩 EFI_Install_USB_for_MateBook_X_Pro_2019-*.zip<BR>
- step3: 打开DiskGenius,左侧选择U盘，选装EFI分区，将EFI_Install_USB_for_MateBook_X_Pro_2019 解压缩后目录拷贝到EFI分区，并重命名为EFI(用其他方式将目录拷贝到EFI分区也可以)  
<B>结束后EFI分区内目录格式，请注意核对</B>

	```
	EFI
	  |----BOOT
	  |      |-BOOTX64.efi
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
- Step7: 将github下载文件中EFI_Install_USB_for_MateBook_X_Pro_2019-*.zip解压缩后拷贝到EFI分区，并重命名为EFI<BR>
不会挂在EFI分区机友，可是使用下载文件中tools目录下"Clover Configurator.zip“，打开软件，左侧选择“挂载分区”，右侧下部选中U盘的EFI，点击挂载分区，此时弹出窗口输入密码，确认即可，在桌面找到EFI盘符可进入
<B>结束后EFI分区内目录格式，请注意核对</B>

	```
	EFI
	  |----BOOT
	  |      |-BOOTX64.efi
	  |----CLOVER
	  |      |-......
	  |      |-......
	```
### 3、现在开始动硬盘了，请一定要备份好数据，可能整个盘数据全丢，尤其是新黑苹果玩家
### 4、调整硬盘分区
这部分出问题最多，很多人又想留着原系统和一键还原。只能自己操作<BR>
强烈建议，这一步使用DiskGenius制作一个WINPE，在winPE下操作,<BR>
强烈建议，把EFI分区备份一下,拷贝到U盘上或者硬盘windows分区内(出现了几例机友,保留了window分区,但是EFI丢失,导致重新安装windows的情况.熟悉windows系统系统的机友可以根据自己经验操作)

硬盘和移动硬盘同样适用
- EFI分区要保证大于200M<BR>
- 使用DiskGenius分一个分区，格式为hpfs+,用于安装mac系统

补充知识：BIOS启动U盘、移动硬盘和硬盘有所不同
- U盘、移动硬盘启动：BIOS查找盘上EFI分区的EFI/BOOT/BOOTX64.efi,进行启动<BR>
- 硬盘启动：硬盘是根据注册到BIOS中的启动项进行启动，BIOS启动项增删改查方式，window有命令BCDEDIT或者用工具EasyUEFI，linux使用efibootmgr命令<BR>

### 5、开始安装
- Step1：开机直接按F2，进入BIOS设置界面
- Step2：关闭相关硬盘启动项。理由：安装过程中全部使用U盘启动，每次开机按F12选择启动菜单来不及
- Step3：关闭安全启动
- Step3：确保软件安全芯片打开;否则会无限重启
- Step4：使用PM981硬盘的机友，安装到移动硬盘上，请关闭设置界面下半部分的HDD设备。理由：PM981会造成不定时重启，增加安装难度
- Step5：F10保存，重启
- step6、按F12选择U盘启动
- step7、进入安装过程<BR>
这部分我就不写了，这部分网上教程很多。<BR>
  #### 容易出现问题：<BR>
- 1）无法选择安装盘，一般是分区抹盘失败/EFI小于200M
- 2）抹盘失败基本是分区没搞好


### 6、安装后处理(请确认已经可以进入OSX桌面,此时由于未驱动显卡字体很少,机器卡顿)
#### 替换启动EFI文件（使用替换后EFI启动）
- Step1: 打开U盘EFI分区；下载文件中tools目录下“Clover Configurator.zip"，打开软件，左侧选择“挂载分区”，右侧下部选中U盘的EFI分区，点击挂载分区，此时弹出窗口输入密码，确认即可，在桌面找到EFI盘符可进入 
- step2: 进入EFI分区，EFI目录将Clover目录改名为“CloverInstall”
- step3: 把github下载的EFI_for_MateBook_X_Pro_2019-*.zip解压缩，并将其中CLOVER复制到EFI分区EFI目录下
- step4: 重启(如果失败就进群咨询,极有可能是bios区别造成的)
- step5: 效果确认(功能键与windows设置功能键优先和Fn键是否亮有关,组合配置功能有4种,自己试)
  - 显卡：字体图标比上一次启动增加1倍，左上角点击苹果图标->关于本机，确认显示内存为超过1G；F1功能键可以调节显示器亮度
  - 电源：左上角点击苹果图标->系统偏好设置->节能，勾选下方“在菜单栏显示电池状态”，屏幕右上角可以看到电池图标机充电状态
  - 触摸板：左上角点击苹果图标->系统偏好设置->触摸板
  - 触摸屏：直接用手测试
  - 声卡：左上角点击苹果图标->系统偏好设置->声音，可以听到声音，f5/f6功能键可以调节声音大小，此时耳机听音乐只有伴奏，无人声或很小(声音平衡调整左或者右可解)
  - 蓝牙：此时不可用。
### 6、安装优化
#### 显卡(如果有外接4K显示器需求)
  由于bios预分配显存默认配置为32M,外接4K是需要修改bios隐藏配置将预分配显存修改为64M.DVMT32不支持外接4K显示器-结果是外接显示器最大支持2560*1440, <BR>修改BIOS隐藏配置参见MatebookXPro2019_黑果包中<Matebook_X_pro_2019设置dvmt.txt>说明.<BR>
  Clover中两套配置DVMT32M和DVMT64M,默认为DVMT32M

#### 处理蓝牙
- Step1:安装VMware fusion,
- Step2:解压蓝牙启动工具.zip
- Step3:双击执行蓝牙脚本目录的 install.command
- Step4:重新启动
	安装脚本会在桌面创建"蓝牙启动.command",开机或蓝牙不能连接时，可以双击脚本重新驱动蓝牙，<BR>
#### 处理启动啰嗦模式界面
  打开EFI分区EFI/CLOVER/config.plist;下面一段删除-V
 ```
  <key>Boot</key>
	<dict>
		<key>Arguments</key>
		<string>-v -cdfon -igfxmlr dart=0</string>
	</dict>
  ```
  <B>删除-v即可</B>
#### 进入Clover界面直接启动
 打开EFI分区EFI/CLOVER/config.plist;找到下面一段,
 - 修改LastBootedVolume为苹果分区卷标
 - false改为true.

 ```
	<key>Boot</key>
	<dict>
		<key>Arguments</key>
		<string>-cdfon -igfxmlr</string>
		<key>DefaultVolume</key>
		<string>LastBootedVolume</string>
		<key>Fast</key>
		<false/>
		<key>Timeout</key>
		<integer>5</integer>
	</dict>
 ```
#### 自己生成SMBIOS
  原因：此时使用SMBIOS可能很多人使用，导致appstore安装软件存在问题
- step1:下载文件中tools目录下“Clover Configurator.zip"，打开软件
- step2:左侧选择“机型设置”，右边窗口在“检查覆盖范围下方”有个上下箭头的小按钮，点击后弹出菜单，选择“Macbook Pro 1.5.2”
- step3:顶部菜单选择“存储”，弹出保存对话空，在“位置”右侧有一个向下的那就，点击后选择存储目录，修改文件名
- step4:使用文本编辑器打开刚才存储的文件，将SMBIOS一段复制到目前启动U盘的EFI/CLOVER/config.plist总相同的位置
## 六、安装完成，请使用验证

## 七、调整硬盘启动（默认你已经会打开EFI分区）
- 将目前启动U盘的EFI目录下CLOVER目录复制到硬盘的EFI目录下
- 重新启动到WIN，使用EasyUEFI，添加启动为，启动文件为CLOVERX64.efi
- 如果安装开始在BIOS中已关闭硬盘启动，则在BIOS设置中打开硬盘启动。
- 修改后可以不使用U盘启动，在开机是按F12打开启动菜单，选择启动项即可启动
另有多重启动菜单方式,参见库上bootmenu目录.
