### 我个人的一些脚本

- [inexistence 盒子部署一键脚本](https://github.com/Aniverse/inexistence)  
可以在有 root 权限、运行主流 LTS 版本的 Debian/Ubuntu 服务器上，安装 qb/tr/rt/de 客户端  
- [AccTCP 网络优化脚本](https://github.com/Aniverse/TrCtrlProToc0l)  
说白了就是安装 bbr／魔改 bbr／bbrplus／锐速的多合一脚本  
- [iFeral 共享盒子专用脚本](https://github.com/Aniverse/iFeral)  
我目前没啥精力维护这个脚本，很多功能有问题……  
- [bluray 转发原盘专用脚本](https://github.com/Aniverse/bluray)  
可以对 BDMV/BDISO 扫 bdinfo、截图、制作种子的一键脚本  
- [Abench](https://github.com/Aniverse/A)  
服务器测试脚本，主要优势在于可以检测独服的硬盘通电时间，使用 fio 测试 SSD 性能  
- [aBox](https://github.com/Aniverse/aBox)  
各种脚本杂烩，包含了一键配置 IPv6 脚本、iperf 测速脚本、更换 r8168 驱动脚本等  
- [qbittorrent-nox-static](https://github.com/Aniverse/qbittorrent-nox-static)  
在十几秒内安装好静态编辑的 qbittorrent-nox 并进行配置，适配 CentOS／Fedora／Debian／Ubuntu／ArchLinux／OpenSUSE  

### 云文档

- [PT 限盒／限 IP／HR 情况统计表](https://kdocs.cn/l/sEi6Sg5iu)  
- [个人评出的高性价比 seedbox 统计](https://kdocs.cn/l/sNHCWHL2J)  

### 常见独服／盒子购买网址

- [OneProvider](https://oneprovider.com/dedicated-servers/paris-france)  
简称 op。作为盒子使用时一般买的都是 OP 法国巴黎的机器，巴黎的机器基本都是转卖的 Scaleway 的机器  
廉价机器基本都是过时硬件，硬盘通电时间 3-7 万小时都是常有的事情，这价格也不能要求太多。  
他家还有其他地区的机器，但刷流而言性价比一般都不如巴黎的。比如荷兰阿姆斯特丹的部分机器也是 Scaleway 的机器，但一般价格比巴黎更贵；加拿大蒙特利尔的机器是 OVH 的，不要买，实际上行带宽只有 250Mbps  
- [Online（现 Scaleway）](https://www.scaleway.com/en/dedibox/pricing)  
简称 ol 或 scw，以前叫 Online.net，现在应称之为 Scaleway Dedibox  
这家现在非特价机性价比不行，要么等促销的时候买特价机，要么就去 OP 那边买 SCW 淘汰下来的机器  
国内盒子中大约有一半或者更多使用 scw/op 的服务器，市场占有率还是很高的  
- [Hetzner](https://www.hetzner.com/sb)  
简称 Hz，一般买的都是他家的拍卖机。像 i7 2600 的机器，你看 CPU 就能知道这机器服役很久了，硬盘一般都比较老  
最大特点是真 1Gbps，在这个价位敢说是 1Gbps dedicated and unmetered 的，可能全世界也只有 Hz 一家了。
非拍卖机安装费比较贵，不过在这价格下能买到那种配置性价比也算不错了  
- [OVH](https://www.ovh.ie)  
OVH 是欧洲第一大主机商，在世界范围来看也算数一数二的。价格不便宜，且很多机器带宽也不是真 1Gbps，不适合刷流  
- [SoYouStart](https://www.soyoustart.com/ie)  
简称 sys，算是 OVH 旗下的中低端独服品牌。SYS 目前在售的机器带宽是 250/500M，从 PT 刷流角度而言不推荐购买  
OVH/SYS/KS 用的网络都是一样的，你可以这么理解：OVH 淘汰下来的机器就会扔给 SYS 销售，SYS 都不要的机器就给 KS  
OVH/SYS/KS 是不同的网站，账号不通用，每个站需要单独注册，且现在注册时 country 无法选择 China  
- [Kimsufi](https://www.kimsufi.com/en)  
简称 ks，是 OVH 旗下的低端独服品牌。带宽为 100Mbps，刷流不太好使，不过有些特价机还算值得买。  
- [Ikoula](https://www.ikoula.cn/zh)  
简称 ik。刷国内站的话连接性还算不错，不过 1Gbps 并不是真的无限制，容易被限速  
- [WalkerServers](https://clients.walkerservers.com/aff.php?aff=38) （***本链接含 aff***，[不含 aff 的点此](https://clients.walkerservers.com)）  
简称 WS，销售 Hz/LW/NF 的独服，包优化和技术支持，配置对得起价格，在同类里性价比算很好的了  
什么是 aff？简单来说，你点了这个含 aff 的链接下单购买的话，我有一定的返利。对你没什么坏处，你付的钱还是一样，得到的东西还是一样的，但对我有好处。如果你不愿意走 aff 的话就点不含 aff 的链接下单  


- [Andy10gbit](https://www.reddit.com/user/Andy10gbit)  
这就是传说中的 andy，没官网。包优化和技术支持，价格不如 WS  
一般推荐去 [discord](https://discord.gg/7Gv8tdM) 联系他，不过他回复的速度有时候能慢得令人发指  
你付完钱，他说 24 小时内交付，结果拖了一个多星期才交付都见怪不怪了；有问题问他，可能回复也要等很久  
他偶尔会搞些性价比还不错的促销。另外他卖的 OVH 是你能找到的最便宜的保证带宽 1Gbps 的 OVH 独服  
- [FeralHosting](https://www.feralhosting.com/pricing)  
简称 FH 或 Feral，以前国内很多人用，现在因为不少站禁止共享盒子，用的人不多了  
真无限流量的 20Gbps 共享盒子，能刷多少看你造化以及你的邻居是否凶残  
- [SeedHost](https://seedhost.eu)  
简称 SH。共享盒子和独服都有，刷力较强，网络用的是 LeaseWeb，连接性不错，缺点是限流  
- [UltraSeedBox](https://www.ultraseedbox.com)  
简称 USB，以前用的 YISP 和 NFOrce，刷流挺强；但目前所有在售的套餐全是限流的，以 Plex 为卖点  
现在所使用的 Novo 的网络连接性也不是很好，刷流用的话我不怎么推荐  
- [seedbox.io](https://seedbox.io)  
我个人把它简称为 sbio，这家有独服和共享盒子，共享盒子的 BT 客户端只提供 rTorrent，且无 SSH 权限。  
独服卖的是 LW/NF 的，但性价比不如 WS 和 SH  
- [seedboxes.cc](https://seedboxes.cc/)  
我个人把它简称为 sbcc，似乎需要梯子才能访问。为数不多的 10/20Gbps 无限流量共享盒子  
- [PulsedMedia](http://pulsedmedia.com/clients/aff.php?aff=1230)（***本链接含 aff***，[不含 aff 的点此](https://pulsedmedia.com)）  
简称 PM。虽然我给了 aff 链接，但说句真心话，我觉得这家挺垃圾的，刷流就算了，保种还算能用  
这家的连接性非常差，客户端也仅提供了 rTorrent，价格也不美丽。但偶尔搞出的特价机的性价比还是挺不错的  


- [LeaseWeb](https://www.leaseweb.com)  
简称 LW。SH/WS/sbio/andy 的很多机器都来自这家。官网价格比 reseller 卖的价格贵得多，不要从官网购买  
在国外刷子眼中，使用 LW 网络的盒子在刷流竞速中最强，不过由于限流且加流量很贵，不推荐刷需要大流量的站  
- [NFOrce](https://www.nforce.com)  
简称 NF。WS/sbio/andy 的很多机器都来自这家。官网价格比 reseller 卖的价格贵得多，不要从官网购买  
NF 的网络质量也还算不错，虽然也限流，不过只计算上行流量，加流量价格也比 LW 便宜  

### 其他 seedbox 脚本

- [QuickBox](https://quickbox.io)  
这个脚本的[社区版](https://github.com/QuickBox/QB)（CE，开源免费）现在基本不更新了，作者专注于维护专业版（Pro，不开源）  
QuickBox Pro 可以算是最强盒子脚本了，然而每台机器 5 美元每月的价格，很多用户不会买账  
事实上我觉得免费的 swizzin 或者 quickbox-lite、inexistence 也比较够用了，花钱买 QuickBox Pro 不是很有必要  
- [QuickBox-lite](https://github.com/amefs/quickbox-lite)  
efs 巨佬维护的 quickbox 脚本，dashboard 好用，更新、维护及时，推荐使用  
- [QuickBox-arm](https://github.com/amefs/quickbox-arm)  
efs 巨佬维护的 quickbox-lite 脚本的 arm 分支，专门用于 ARM 架构的设备（如树莓派）  
- [swizzin](https://swizzin.ltd)  
QuickBox CE 版停更后，swizzin 算是英文社区里最强的免费开源盒子脚本了，用户很多，口碑良好  
支持多用户、支持网页面板上一键安装不少软件（但不支持安装 qBittorrent）  
- [PGBlitz (AKA PlexGuide)](https://plexguide.com/forums/)  
基于 Docker 部署软件的脚本，这个脚本更侧重于搭建媒体服务器，而不是构建 seedbox  

### Discord channels for seedbox/trackers

[swizzin](https://discord.gg/bDFqAUF)  
[QuickBox](https://discordapp.com/invite/hCCbVhu)  
[Reddit r/seedboxes](https://discord.gg/THMNRuX)  
[UltraSeedBox](https://discordapp.com/invite/yFcV8EN)  
[andy10gbit](https://discord.gg/7Gv8tdM)  
[WalkerServers](https://discord.gg/wv67teS)  
[cloudboxes.io](https://discordapp.com/invite/vHnKR68)  

### Hetzner 独服一键安装系统（软 RAID0）

注意：这个方法只适用于软 RAID（**不支持硬 RAID**）、多硬盘且**所有硬盘大小相同**的 Hetzner 独立服务器。  
比如 2 块 3TB HDD、4 块 4TB HDD、2 块 NVMe SSD 等都可以用这个命令；但是对于 SSD+HDD 或者 1T SSD + 2T SSD 之类的特殊情况请不要使用这个命令  
在 hz 的控制面板里开启 rescue（救援模式） 后再在 reset 里重启服务器，之后 SSH 连接服务器，直接输入下面的一行命令就可以了  

```
# 安装 Debian 9
echo x | installimage -p /boot:ext3:1G,/:ext4:all -l 0 -r yes -i images/Debian-911-stretch-64-minimal.tar.gz -a -n Hz && reboot

# 安装 Debian 10
echo x | installimage -p /boot:ext3:1G,/:ext4:all -l 0 -r yes -i images/Debian-105-buster-64-minimal.tar.gz  -a -n Hz && reboot

# 安装 Ubuntu 16.04
echo x | installimage -p /boot:ext3:1G,/:ext4:all -l 0 -r yes -i images/Ubuntu-1604-xenial-64-minimal.tar.gz -a -n Hz && reboot

# 安装 Ubuntu 18.04
echo x | installimage -p /boot:ext3:1G,/:ext4:all -l 0 -r yes -i images/Ubuntu-1804-bionic-64-minimal.tar.gz -a -n Hz && reboot

# 安装 Ubuntu 20.04（inexistence 尚不支持该系统）
echo x | installimage -p /boot:ext3:1G,/:ext4:all -l 0 -r yes -i images/Ubuntu-2004-focal-64-minimal.tar.gz  -a -n Hz && reboot
```

相比其他教程，这个命令的优点在于完全不需要任何交互操作，不需要修改分区、选择系统等等，复制——粘贴——敲回车就搞定了。  
