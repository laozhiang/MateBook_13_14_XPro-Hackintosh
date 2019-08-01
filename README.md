# Matebook X Pro 2019 黑苹果教程

记录Matebook X Pro黑苹果过程
本文仅记录黑苹果过程，不涉及多系统安装。
目前仅仅是个半成品、请大家一同改进

## 一、机型配置信息
| 项目 | 详细参数|
| :--: | :-------------------- |
| 型号 | Matebook X Pro 2019 i5 集显版   |
| CPU  | i5 8265u |
|内存| DDR3L 8G|
| 显卡 | UHD620|
| 硬盘 | 更换为 Intel P760(据说三星PM981 不支持黑苹果)|
| 声卡 | Realtek ALC256 |
|LCD| 3000*2000|
|BIOS|1.15|
## 二、成果
| 项目 | 成果|
| :--: | :-------------------- |
| 版本 | Mac OSX Majave 10.14.5
| 显示   | 内屏OK<BR>DP外接屏NOK<BR>HDMI外接屏无设备未测试<BR>可修改仿冒ID，调整接口数据进行实验 |
| 声音   | OK，外放耳机自动切换OK |
| 触摸屏 | OK |
| 触摸板 | OK |
| 键盘调亮度 | 未处理 |
| 键盘调音| OK,静音键现实图标，但不能静音 |
| 电源   | NOK |
| WIFI  | NOK |
| 蓝牙   | NOK|
| 摄像头 | NOK |
## 三、问题记录
- 启动：不定期启动不成功，更换OsxAptioFix3Drv.efi，正在尝试中，尝试成功后修改
- 电源：采用VirtualSMC+SMCBatteryManager读取数据为空（ECRD读取寄存器不成功，寄存器未初始化）
- 摄像头：据说碰运气。个人无用不再处理
- 蓝牙：个人使用usb蓝牙适配器，不处理，猜测参照 Matebook X pro 2018机型处理即可
## 四、安装需求
USB Hub或扩展坞(该机型仅有1个USB接口，安装需要两个USB设备)
U盘 8G以上
USB鼠标 

## 三、软件下载

## 四、安装U盘制作
### 1、苹果系统下制作
### 2、windows下制作

## 五、安装用Clover制作
### 1、使用github上文件
  - Step1: 在U盘EFI分区下新建EFI目录
  - Step2: 将CLOVER_for_Install_USB拷贝到U盘EFI分区下EFI目录下，并改名为CLOVER
  - Step3: 在U盘EFI分区EFI目录下新建BOOT目录
  - Step4: 将EFI\CLOVER下CLOVERX64.efi复制到BOOT目下，并改名为BOOTX64.efi
### 2、个人手工制作
此节记录CLOVER目录制作过程，采用已制作好文件，跳过此节。

暂时不写，后续补充
## 六、安装 MAC OS X
这个就不写了，直接网上去搜。

注意点，就是硬盘EFI分区一定要大于200M
## 七、打系统补丁
- Step1: 用安装USB盘启动，将patch下的AppleIntelCFLGraphicsFramebuffer.kext复制到系统S/L/E目录下
-  Step2:启动KextUtility，自动重建驱动cache
## 八、更新Clover目录
- Step1:将CLOVER复制到硬盘EFI分区EFI目录下
- Step2:添加BIOS启动项
  - windows下采用easyuefi
  - linux采用efibootmgr命令添加
## 九、安装后处理
### 1、触摸板轻触修改为点击
由于没有驱动电源，无法打开触摸板控制板，
采用命令行开启，因为有sudo，建议一下命令逐个执行

···
defaults write com.apple.AppleMultitouchTrackpad Clicking -bool true
sudo defaults write com.apple.driver.AppleBluetoothMultitouch.trackpad Clicking -bool true
sudo defaults -currentHost write NSGlobalDomain com.apple.mouse.tapBehavior -int 1
sudo defaults write NSGlobalDomain com.apple.mouse.tapBehavior -int 1
···
## 十、Clover修改过程