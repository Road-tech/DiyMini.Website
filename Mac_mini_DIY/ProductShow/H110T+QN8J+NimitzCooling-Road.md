# 终于等到你——DIY Mac mini & Hackintosh
Hackintosh for Asus-H110T, 8100, DW1820A, using Opencore and Support macOS Catalina

文章转载至[https://blog.malu.tech/2020/05/06/DIYMacmini&Hackintosh/](https://blog.malu.tech/2020/05/06/DIYMacmini&Hackintosh/)

## BB两句

说好的捋一捋2019捡的垃圾，结果1月底写完第一篇文章就一直没动静了。转眼间大半年过去了，我终于有点闲钱和时间来继续折腾。19年捡的一堆硬件：HP 800 G1 DM，华硕H110t，精英H110S2p，华硕H110S1。4款设备现在终于折腾到了第二款。

不得不说DIY一台Mac mini一直是我的梦想，奈何金钱和能力有限，太复杂太高端的方案一直不敢碰，唯有尼米兹的方案一直很对我胃口：不会太复杂，不粗糙好看。一直很口水上一代尼米兹的散热方案，适配的是华硕H81T。奈何但我发现这款方案的时候，那套尼米兹散热就已经停产了。

万万没想到又出了新的尼米兹的散热方案，可是当我收到了主板的时候，生产这套方案的厂家就因为搬家而停止了。然后就一直等，然后等到天气变冷了，这张3D打印的方案就因为容易卷边就一直搁置。然后就遇上了疫情。一等久等了大半年。在我都绝望准备放弃的时候，万万没想到又重新生产了。第一时间下单，然后又发现原本15块一个的冲压金属网孔底网居然卖完了。咸鱼居然有人开价150块收一个都收不到。一直到最近群里的大佬设计打印了网孔的散热底盖。至此，我才攒出这一台心仪的Diy mini。

然后要感谢mac mini diy 交流群里的两位兄弟：
@梦的猴子-H110T+qn8j 他无情的充当了我的小白鼠，测试了大量的bios，还帮我完善了EFI。
@中二病不接受治疗 感谢大佬设计了Mac mini的散热底盖。

然后说一下华硕H110T这款主板：

支持2230/2242/2260长度的SSD，也就是说常用的2280长度的SSD是不能用的，不够位置。

基本没有2260长度的SSD，2230/2242的SSD性能很一般，一般都是中低端的方案。

但是不用担心，H110T这款主板的M.2插槽只支持X2的速度，用高端的方案也是浪费。

害得我辛辛苦苦找遍全网才找到的2242长度，支持X4速度的NVME SSD，显得毫无意义。

幸好这个diy的SSD用的只是2263XT的无缓低端方案，也跑不满x4。

![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh-AsusH110T-QN8J-I7-8700Tes-DW1820A-OC/000.jpg?raw=true) 

## 硬件

|-----------+-------------------------------------------------------+-------------------------------------------|
|          	|                        型号                        	|                  备注                  	|
|:--------:	|:----------------------------------------------------:	|:----------------------------------------:	|
| 主板     	|                     Asus H110T                     	|                Thin ITX                	|
| 处理器   	|                        QN8J                        	|               I7 8700T ES              	|
| 散热器   	|     Nimitz Diy Mac Mini 3D-printing cooling kit    	|       Nimitz 超盒 3D打印散热套件          	|
| 硬盘     	| 定制SSD 基于 SM2263XT 和 512g Intel TLC NAND Flash 	    |       NVME 固态套料 主控板2263XT         	|
| 内存     	|            SEIWHALE 16G DDR4 2666MHz X2            	|   枭鲸 16G DDR4 2666 笔记本电脑内存条    	|
| 无线网卡 	|                     BCM94350ZAE                    	|                 DW1820A                	|
| 机箱     	|           Mac mini teardown case拆机机箱             	|            Mac mini 拆机机箱             	|
| 电源     	|       Dell 74/50mm 19v 130w DC power adapter       	| Dell 74/50mm 19v 130w DC power adapter 	|
|-----------+-------------------------------------------------------+-------------------------------------------|

## EFI下载地址

跳转至Github  [下载地址](https://github.com/Road-tech/Hackintosh-AsusH110T-QN8J-I7-8700Tes-DW1820A-OC)

**使用EFI前请务必修改三码(SSN,UUID,ROM)**    
**Please change three system codes (SSN,UUID,ROM) before using this EFI**   

## macOS完善情况

### 支持：
- HDMI port (1080p) ｜ HDMI接口
- DP port (1080p) ｜ DP接口
- Audio output on HDMI ｜ HDMI接口音频输出
- All USB ports ｜ 所有USB接口
- Wi-Fi & Bluetooth ｜ Wi-Fi & 蓝牙
- Dual Network Interface Card ｜ 双网口
- 3.5mm Audio Output & Mic Input ｜ 3.5mm音频输出
- Airdrop ｜ 隔空投送
- AirPlay ｜ 投屏
- Continuity ｜ 接力   

### 不支持:
- hyper-threading ｜ 超线程

### 未测试:
- Sleep ｜ 睡眠
- 4k display ｜ 4K输出  （我没有4K屏）

## 备份MAC地址: 

华硕H110T这块主板有两张网卡：

* Realtek® RTL8111H  
* Intel® I219V  

华硕把Intel网卡的MAC地址写在了BIOS里面，但是在为了支持8代CPU去魔改BIOS之后，会丢失Intel网卡的MAC地址。 具体表现为Intel网卡的MAC地址会变成```88:88:87:88```，所以要先备份MAC地址。

有两个方法去查MAC地址：

* 主板的内存槽上贴着MAC地址，Intel网卡通常是左边那个
* Windows下用 ```ipconfig``` 或者 macOS/Linux下用 ```ifconfig```去查MAC地址

![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh-AsusH110T-QN8J-I7-8700Tes-DW1820A-OC/100.jpg?raw=true)  

## 刷入魔改BIOS

BIOS在上图左下角红框的位置，拔下来刷入。
**必须用编程器刷入BIOS！**

我尝试了两个BIOS：

1. 我我现在在用的，6核以上无法打开超线程，6核以下如8100没有问题。能安装macOS，[下载地址](https://raw.githubusercontent.com/Road-tech/Hackintosh-AsusH110T-QN8J-I7-8700Tes-DW1820A-OC/master/ASUSTeK_H110T_3805HT.bin)
2. D大修改的BIOS，可以打开超线程，但是无法安装macOS（我还在尝试修复），会报错 ```ACPI Error: [\_SB_.PCi0.XHC_.RHUB.HS11] namespace lookup failure, AE_NOT_FOUND ```   如果你不需要安装macOS，请直接使用这个。 [下载链接](http://www.smxdiy.com/thread-1862-1-1.html)

D大的bios引导报错，我尝试打开了XCHI-hand off，没有效果。我也尝试修改DSDT屏蔽HS11，但是似乎没有效果，不知道是不是我操作有问题。

在这里请求各位大佬，能不能帮我修复下修复无法打开超线程的bug，我这里提取了两个bios下的DSDT，可以下载去比对一下看看能不能修复。[下载地址](https://github.com/Road00/Hackintosh-for-Asus-H110T-QN8J-I7-8700T-ES-DW1820A-using-Opencore-and-Support-macOS-Catalina)       

或者教教我如何屏蔽整个RHUB，我定制了USB之后貌似用不到RHUB下的接口。

## 恢复MAC地址

请准备以下工具：

* 任意容量的U盘      
* Rufus  		[下载地址](https://rufus.ie/zh_CN.html)     
* EEUPDATE 	[下载地址](https://raw.githubusercontent.com/Road-tech/Hackintosh-AsusH110T-QN8J-I7-8700Tes-DW1820A-OC/master/Eeupdate.rar)    

恢复MAC地址流程：

1. 打开Rufus，格式化U盘，制作DOS启动盘。
2. 解压并复制EEUPDATA文件到U盘（假设EEUPDATA放在MAC文件夹内）。
3. U盘插入机子，进入BIOS设定U盘启动，进入DOS系统。
4. 输入 ```dir``` 查看文件。
5. 输入  ```cd MAC``` 进去MAC文件夹。
6. 输入  ```eeupdate /nic=1 /mac=XXXXXXXXX``` 恢复MAC地址，```XXXXXXXXX```为你的记录的MAC地址。
7. 提示成功后重启，进任意操作系统查看网卡MAC地址是否恢复成功。

## BIOS设定：

### Disable/禁用：
- Fast Boot  
- CFG Lock   
- VT-d  
- CSM  
- Intel SGX  

### Enable/启用：
- Intel Virtualization Technology   
- Above 4G decoding  
- Hyper Threading 
- Serial Port 
  
## 安装macos

请准备以下工具：
* 系统镜像：【Len's DMG】macOS Catalina 10.15.2 19C57 With Clover 5100 and OC 0.5.2镜像 [下载地址](http://bbs.pcbeta.com/forum.php?mod=viewthread&tid=1836586)    
* OC编辑工具：OpenCore Configurator [下载地址](https://mackie100projects.altervista.org/)    
* 镜像写入工具：Etcher （Windows，macOS，Linux皆可运行） [下载地址](https://www.balena.io/etcher/)    
* 我提供的OC引导的EFI：[下载地址](https://github.com/Road-tech/Hackintosh-AsusH110T-QN8J-I7-8700Tes-DW1820A-OC)    
* 准备一个大于10g的u盘    

安装过程我就不重复了，大家可以参考下[我之前的文章](https://post.smzdm.com/p/adwrg48d/)。

安装完成后请记得模拟NVRAM：
请在安装完系统后将增加 **LogoutHook** 文件用于放置在任意位置。并且在终端输入：
 ```sudo defaults write com.apple.loginwindow LogoutHook /path/to/LogoutHook.command```

比如你放在**下载**文件夹内： 
```sudo defaults write com.apple.loginwindow LogoutHook /Users/xjn/Documents/LogoutHook/LogoutHook.command```

重启后，你会在/EFI/下看到nvram.plist，代表已经成功模拟了。

**！运行后不要删除补丁包 ！**

## 成品展示

![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh-AsusH110T-QN8J-I7-8700Tes-DW1820A-OC/001.jpg?raw=true)  
全家福
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh-AsusH110T-QN8J-I7-8700Tes-DW1820A-OC/002.jpg?raw=true)  
QN8J，35w，6核12线程，1.6GHz默频
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh-AsusH110T-QN8J-I7-8700Tes-DW1820A-OC/003.jpg?raw=true)  
屏蔽+短接
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh-AsusH110T-QN8J-I7-8700Tes-DW1820A-OC/004.jpg?raw=true)  
硬件合体，不知道枭鲸知不知道他家的内存贴纸贴反了
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh-AsusH110T-QN8J-I7-8700Tes-DW1820A-OC/005.jpg?raw=true)  
请出尼米兹散热器
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh-AsusH110T-QN8J-I7-8700Tes-DW1820A-OC/006.jpg?raw=true)  
将弹簧放在风道主体，然后把纯铜散热器压上去
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh-AsusH110T-QN8J-I7-8700Tes-DW1820A-OC/007.jpg?raw=true)  
把散热背板放在主板后面，然后把风道主体压上去，最后上螺丝拧紧。
这一步超级反人类！假象一下，弹簧并不能固定在主体上，散热器也不能，你要把它倒扣在主板上还要保证主体-弹簧-散热之间不能移位。最后你还要确保主体的螺丝孔能够对得上散热器的背板。
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh-AsusH110T-QN8J-I7-8700Tes-DW1820A-OC/008.jpg?raw=true)  
这个安装反人类到我不想装第二次！ 所以请尽量保证机子可以正常开机后再进行装机。
**请务必注意四颗螺丝的受力尽量均匀且不会过紧，不然可能会压弯主板！**
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh-AsusH110T-QN8J-I7-8700Tes-DW1820A-OC/009.jpg?raw=true)  
装上后IO板之后就可以推进机箱了！同时别忘了接上Wi-Fi天线。
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh-AsusH110T-QN8J-I7-8700Tes-DW1820A-OC/010.jpg?raw=true)  
成功合体！推入过程不会太顺畅的，要按压一下，刚刚能推进去。
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh-AsusH110T-QN8J-I7-8700Tes-DW1820A-OC/011.jpg?raw=true)  
最后装上风扇，这里可以看到3d打印的纹路，很粗糙
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh-AsusH110T-QN8J-I7-8700Tes-DW1820A-OC/012.jpg?raw=true) 
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh-AsusH110T-QN8J-I7-8700Tes-DW1820A-OC/013.jpg?raw=true) 
接下来就是重量嘉宾，大佬设计打印的网孔底盖！
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh-AsusH110T-QN8J-I7-8700Tes-DW1820A-OC/014.jpg?raw=true) 
还是很精致漂亮的
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh-AsusH110T-QN8J-I7-8700Tes-DW1820A-OC/015.jpg?raw=true) 
完美装上，严丝合缝
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh-AsusH110T-QN8J-I7-8700Tes-DW1820A-OC/016.jpg?raw=true) 
换个角度
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh-AsusH110T-QN8J-I7-8700Tes-DW1820A-OC/017.jpg?raw=true) 
装上小辣椒天线
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh-AsusH110T-QN8J-I7-8700Tes-DW1820A-OC/018.jpg?raw=true) 
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh-AsusH110T-QN8J-I7-8700Tes-DW1820A-OC/019.jpg?raw=true) 
成品展示
![image](https://cdn.jsdelivr.net/gh/Road-tech/Road-blog-Figure@1.0/Hackintosh-AsusH110T-QN8J-I7-8700Tes-DW1820A-OC/102.PNG?raw=true) 

## 参考链接

[精解OpenCore](https://blog.daliansky.net/OpenCore-BootLoader.html) - [黑果小兵的部落阁 ](https://blog.daliansky.net/)

[使用OpenCore引导黑苹果](https://blog.xjn819.com/?p=543) - [XJN](https://blog.xjn819.com/) 

[Asrock deskmini 310-com hackintosh 10.14-10.15 EFI](https://blog.xjn819.com/?p=7) - [XJN](https://blog.xjn819.com/)

[DW1820A/BCM94350ZAE/BCM94356ZEPA50DX插入的正确姿势](https://blog.daliansky.net/DW1820A_BCM94350ZAE-driver-inserts-the-correct-posture.html) - [黑果小兵的部落阁](https://blog.daliansky.net/)

[华硕 ASUS H110T 支持 8 代 9 代 Xeon BIOS](http://www.smxdiy.com/thread-1862-1-1.html) - [D大](http://www.smxdiy.com/space-uid-1196.html)
