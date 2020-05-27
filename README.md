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
在几十秒内安装好静态编辑的 qbittorrent-nox 并进行配置，适配 CentOS／Fedora／Debian／Ubuntu／ArchLinux／OpenSUSE  

### 云文档

[PT 限盒／限 IP／HR 情况统计表](https://kdocs.cn/l/sEi6Sg5iu)  
[个人评出的高性价比 seedbox 统计](https://kdocs.cn/l/sNHCWHL2J)  

### Discord channels for seedbox/trackers

[swizzin](https://discord.gg/bDFqAUF)  
[QuickBox](https://discordapp.com/invite/hCCbVhu)  
[Reddit r/seedboxes](https://discord.gg/THMNRuX)  
[UltraSeedBox](https://discordapp.com/invite/yFcV8EN)  
[andy10gbit](https://discord.gg/7Gv8tdM)  
[WalkerServers](https://discord.gg/wv67teS)  
[cloudboxes.io](https://discordapp.com/invite/vHnKR68)  

### 常见独服／盒子购买网址

[OneProvider](https://oneprovider.com/dedicated-servers/paris-france) 简称 op。作为盒子使用时一般买的都是 OP 法国巴黎的机器    
[Online（现 Scaleway）](https://www.scaleway.com/en/dedibox/pricing) 简称 ol 或 scw，以前叫 Online.net，现在应称之为 Scaleway Dedibox  
[Hetzner](https://www.hetzner.com/sb) 简称 Hz  
[OVH](https://www.ovh.ie)  
[SoYouStart](https://www.soyoustart.com/ie) 简称 sys  
[Kimsufi](https://www.kimsufi.com/en) 简称 ks  
[Ikoula](https://www.ikoula.cn/zh) 简称 ik  

[Andy10gbit](https://www.reddit.com/user/Andy10gbit) 也就是 andy  
[FeralHosting](https://www.feralhosting.com/pricing) 简称 FH 或 Feral  
[SeedHost](https://seedhost.eu) 简称 SH  
[UltraSeedBox](https://www.ultraseedbox.com) 简称 USB  

[seedbox.io](https://seedbox.io) 我个人把它简称为 sbio  
[seedboxes.cc](https://seedboxes.cc/) 我个人把它简称为 sbcc，似乎需要梯子才能上  
[PulsedMedia](https://pulsedmedia.com) 简称 PM。这家我个人觉得很垃圾  

### 其他 seedbox 脚本

[QuickBox](https://quickbox.io)  
[QuickBox-lite](https://github.com/amefs/quickbox-lite)  
[QuickBox-arm](https://github.com/amefs/quickbox-arm)  
[swizzin](https://swizzin.ltd)  
[PGBlitz (AKA PlexGuide)](https://plexguide.com/forums/)  

### Hetzner 独服一键安装系统（RAID0）

注意：这个办法只适用于有多个硬盘且每个硬盘大小相同的 Hetzner 独立服务器。比如 2 块 3TB HDD，4 块 4TB HDD，2 块 NVMe SSD 等都可以用这个命令。但是对于 SSD+HDD 或者 1T SSD+2T SSD 这种特殊情况请不要使用这个命令，会造成空间的浪费  
在 hz 的控制面板里开启 rescue（救援模式），reset 里重启服务器，之后 SSH 连接服务器，直接输入下面的一行命令就可以了  
相比其他教程，这个命令的优点在于完全不需要任何交互操作，不需要修改分区、选择系统等等，复制——粘贴——敲回车就搞定了  

```
# 安装 Debian 8（不推荐，系统太老了）
time echo x | installimage -p /boot:ext3:1G,/:ext4:all -l 0 -r yes -i images/Debian-811-jessie-64-minimal.tar.gz  -n Hz -a && reboot

# 安装 Debian 9
time echo x | installimage -p /boot:ext3:1G,/:ext4:all -l 0 -r yes -i images/Debian-911-stretch-64-minimal.tar.gz -n Hz -a && reboot

# 安装 Debian 10
time echo x | installimage -p /boot:ext3:1G,/:ext4:all -l 0 -r yes -i images/Debian-103-buster-64-minimal.tar.gz  -n Hz -a && reboot

# 安装 Ubuntu 16.04
time echo x | installimage -p /boot:ext3:1G,/:ext4:all -l 0 -r yes -i images/Ubuntu-1604-xenial-64-minimal.tar.gz -n Hz -a && reboot

# 安装 Ubuntu 18.04
time echo x | installimage -p /boot:ext3:1G,/:ext4:all -l 0 -r yes -i images/Ubuntu-1804-bionic-64-minimal.tar.gz -n Hz -a && reboot
```


