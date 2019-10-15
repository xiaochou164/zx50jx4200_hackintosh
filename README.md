# Asus ZX50J

zx50jx4200_hackintosh
华硕zx50jx4200 黑苹果EFI配置 可适用于macos 10.15
## 配置：

CPU：Intel i5-4200h

内存：8G 

显卡：Intel HD 4600 + GTX950M(已屏蔽）

外存：东芝120G m.2 SSD + 原厂1t机械

网卡/蓝牙：无线网卡蓝牙更换为 DW1560 NGFF接口


注：如果没有更换dw1560网卡（如果打算长期使用黑苹果并打算使用隔空投送的话建议更换网卡）

删除Clover/kexts/others下面四个驱动
AirportBrcmFixup.kext 
FakePCIID_Broadcom_WiFi.kext 
BrcmFirmwareData.kext
BrcmPatchRAM2.kext 
并搜索原装AR9565或自己的网卡的驱动方法

## 目前bug 
```
1.fn+F1会导致睡死 （请勿尝试!）

2.clover启动设置1080P分辨率开机画面闪现15苹果花屏 (已经降低clover分辨率，解决该问题）

3.无法使用pppoe拨号 未测试

4.HDMI音频有输出，但是会破音 （很久没测试了。可能驱动更新修复了）

5.睡眠不正常（10.14.6是正常的）

6.未知bug
```
2019年10月16日重新提取dsdt、ssdt

音频输入需要用工具修复
变频正常
屏幕亮度正常
键盘灯正常  
Fn快捷键正常

10.14.6下启用睡眠需要关闭bios的CPU节能功能
bios中关闭power off energy saving

## 其他辅助技巧
1.打开安全和隐私中的任何来源 
终端输入 
```
sudo spctl --master-disable
```
### 2.建立一个在Win和Mac下都能读取的分区

在win系统下自带的磁盘管理工具中压缩一个适量空间的分区然后新建简单卷分配盘符然后格式化为exFAT格式,这个分区的内容在win和mac系统下都能读取。）


### 3.修复声卡输入 

使用麦克风修复目录下载教程修复


### 4.查看加载的驱动
显示除了苹果之外的驱动加载
```
kextstat | grep -v "com.apple"      
```
查看加载的非官方驱动
```
kextstat | grep -v "com.apple" | grep -v "Energy"   
```
### 5.解决在低分屏上字体发虚需要做两件事情：

打开 【终端】应用，输入下面命令，全局启用 次像素抗锯齿 渲染：
```
defaults write -g CGFontRenderingFontSmoothingDisabled -bool NO
```
设置字体 次像素抗锯齿 级别 (类似 Linux 的 hintstyle 微调样式) 的命令：
```
defaults -currentHost write -globalDomain AppleFontSmoothing -int 3
```
还原命令为：
```
defaults write -g CGFontRenderingFontSmoothingDisabled -bool YES
```
```
defaults -currentHost delete -globalDomain AppleFontSmoothing
```

