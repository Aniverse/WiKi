# RSS 教程，未完待续
> To be completed ...

首先，本文作者水平也不咋样，欢迎各位大佬们补充、指正错误，求轻喷  
其次，由于篇幅和作者水平有限，很多更进一步的用法你需要自己研究，可以看官方文档甚至是软件的源码（因为有时候官方文档写得不够清楚……）  
然后，如果有大佬看上本文需要转载的，请注明出处  

另外在阅读本文之前，你需要知道的：
1. 本教程只讲解 RSS，AutoDL-Irssi 不在本文范围内，也不要问我什么时候写 AutoDL-Irssi 的教程
2. 本文还没有写完！！！

## 0. 碎碎念

在我所知范围内，Seedbox 上的 RSS 方式主要有以下几种：
1. ruTorrent RSS 插件实现 RSS
2. Flexget 实现 RSS，种子文件下载到 BT 客户端监控目录或者直接推送到 BT 客户端
3. Deluge 使用 YaRSS2 插件 RSS
4. qBittorrent 使用自带 RSS
5. Flood RSS
6. uTorrent 自带 RSS
7. 脚本 RSS

本人的一些点评
1. 上手简单，功能也足够强大，regx、cookies，url_rewrite 都支持。种子直接添加到 rTorrent，之后可以将 Deluge、qBittorrent 的监控目录设定成 rTorrent session 目录来实现 ruTorrent 给 De/qB RSS
2. 功能很强大，本菜鸡表示很多进阶用法其实我都不会（不过简单的用法足够应付不少情况了）  ┓( ´∀\` )┏  
3. Deluge YaRSS2 插件不支持 WebUI，只能配合 ThinClient 使用。过滤功能一般，RSS 间隔最小也要 5 分钟 1 次，不太够用，不是很推荐
4. 估计在盒子上使用 qBittorrent 自带 RSS 功能的人很少，因为 qBittorrent 的 RSS 功能目前在官方的 WebUI 上还没有实现，WebAPI 是有了但似乎还没见到有人做，我看还是得等官方来做这个功能了  
如果你用 Linux 桌面环境，安装 qBittorrent GUI 版本，在桌面环境下配置 RSS，再开一个 WebUI 来远程操作的话倒也是可以（另外如果在 GUI 下配置了 RSS，直接把配置文件内容写到 nox 上似乎也可以，我还没测试过）。不过话说回来， qBittorrent 本身的 RSS 功能我觉得也不够强大……
5. Flood 的 RSS 功能比起来 ruTorrent 还是要弱不少，不知道有多少人在用
6. uTorrent Server 基本上没几个 PT 站允许使用的，官方也弃更了，RSS 也不好用，不讨论；wine uTorrent 我没怎么试过，感觉也不是很有必要。剩下的基本就是 Windows uTorrent 用户了，这类用户也不多  
7. 用脚本 RSS 一般是两种情况：1. 站点没提供 RSS 和 AutoDL-Irssi，只能靠脚本抓取新种子；2. 站点提供的 RSS 无法满足用户的需求（比如你想 RSS Cinematik 的 CC 种子，你用自带的 RSS 就做不到，因为 RSS 源里就不包含种子是否是 CC 的信息）
这类脚本一般都需要对特定站点进行定制，没有通用脚本（顶多一个架构下的不同站点适配，全适配不可能）  

最常见的是 ruTorrent RSS，Flexget RSS 在国内盒子用户里使用率还行但是似乎国外用的不多（仅仅是我的猜测，因为很多脚本都不提供 Flexget 的安装，Seedbox Provider 也基本上没有提供 Flexget 的预装或者一键安装的？）  

本文目前只介绍 ruTorrent RSS 和 Flexget RSS  

# 1. 寻找 RSS 源

我刷过的绝大多数站点都提供了 RSS 功能，有的站点的 RSS 功能比较强大（比如 AvistaZ 系列），有的比较简陋（比如 AsianDVDClub），但总比没有强（比如 HD-Spain 就没 RSS）。  
有时候站点有 RSS 却不能被轻易找到，甚至索性有的站点页面上就找不到 RSS 的按钮。我个人推荐查看页面源代码的方式寻找 RSS 源，这个办法寻找 RSS 源比较便捷。如果这个办法还没找到，再去页面上看看、FAQ/WiKi 找找、论坛里搜索看看，都找不到的话基本上可以确定这个站点没提供 RSS 功能。  

一般我们在种子页面寻找 RSS 源，对于 Chrome 浏览器，按下快捷键 `Ctrl+U` 进入到源码浏览，然后按下 `Ctrl+F` 开启页面搜索。一般来说寻找 RSS 的话就搜索 rss 或者 feed，如下图：  

![CG-1](https://github.com/Aniverse/WiKi/raw/master/Images/RSS/How.to.RSS-CG-1.png)

右键复制这个 <u>/rss.xml</u> 的链接地址，即为该站点的 RSS 链接。  
Cinemageddon 的 RSS 链接便是：`http://cinemageddon.net/rss.xml`  
打开这个链接，可以看到如下界面：

![CG-2](https://github.com/Aniverse/WiKi/raw/master/Images/RSS/How.to.RSS-CG-2.png)

第一个种子的链接是：`http://cinemageddon.net/details.php?id=217348`  
显然，这不是种子的下载链接（下载链接一般都是 download.php 之类的，或者什么 linktype=dl，总之一般都和下载这个词有关系）。打开页面后也可以看到，这其实是种子的浏览页面：  

![CG-3](https://github.com/Aniverse/WiKi/raw/master/Images/RSS/How.to.RSS-CG-3.png)

右键复制种子的下载链接，得到这个链接：`http://cinemageddon.net/download.php?id=217348&name=A.Revolucao.de.Maio.1937.720p.WEBRip.x264-MaZ.mkv.torrent`  
观察这个种子下载链接和之前的种子页面链接，其实主要区别就在于 `details.php` 和 `download.php` 上  
把后面的 `name=A.Revolucao.de.Maio.1937.720p.WEBRip.x264-MaZ.mkv.torrent` 替换成 `name=123.torrent`，你下来的文件本身还是一样的，就是文件名不同罢了  
如果你直接用 `http://cinemageddon.net/download.php?id=217348` 下载，会得到 `download.php` 这个文件，但其实这也是一个种子文件，就是后缀名不对罢了  
因此，后边的 `name=XXX` 这一串其实意义不大，我们要做的就是把 `details` 这个词替换成 `download`，这一操作要如何完成，在之后讲解  

再来几个其他站点寻找 RSS 源的例子：

![RSS-HDForever](https://github.com/Aniverse/WiKi/raw/master/Images/RSS/RSS-HDForever.png)
![RSS-WiHD](https://github.com/Aniverse/WiKi/raw/master/Images/RSS/RSS-WiHD.png)
![RSS-Bibliotik](https://github.com/Aniverse/WiKi/raw/master/Images/RSS/RSS-Bibliotik.png)



# 2. 获取 Cookies

**注意**：本教程使用 Chrome 浏览器来讲解，其他浏览器用户请自行搜索获取 Cookies 的办法  

由于某些站点提供的 RSS 里的链接不带 passkey 之类的信息（比如 AsianDVDClub、CinemaGeddon、Cinematik、ILoveClassic），无法直接在盒子上下载种子，因此需要使用 Cookies（ [什么是 Cookies？](https://baike.baidu.com/item/cookie/1119)）  

获取 Cookies 的办法有很多种，比如可以用 [EditThisCookie](https://chrome.google.com/webstore/detail/editthiscookie/fngmhnnpilhplaeedifhccceomclgfbg) 插件导出，或者按照下图操作：

![CG-4](https://github.com/Aniverse/WiKi/raw/master/Images/RSS/How.to.RSS-CG-4.png)  
![CG-5](https://github.com/Aniverse/WiKi/raw/master/Images/RSS/How.to.RSS-CG-5.png)  

这里 Cookies 有三个值，实测 `__cfduid` 不用写也可以用于 RSS  

本文再介绍一种我个人在用的复制 Cookies 的办法：（大佬们如有更便捷的方案，欢迎告知）  

1. Chrome 浏览器，标签页切换到你要获取 cookies 的站点，按下快捷键 `F12` 打开控制台，切换到 Network

![CG-6](https://github.com/Aniverse/WiKi/raw/master/Images/RSS/How.to.RSS-CG-6.png)  

2. 按下 `F5`，刷新页面

![CG-7](https://github.com/Aniverse/WiKi/raw/master/Images/RSS/How.to.RSS-CG-7.png)  

点第一个 `details.php?id=217348`，也就是和网址一样的那个  

3. 直接复制 `Request Headers` 里 `Cookies` 那一栏就可以了。值得注意的是 `User-Agent`，有些情况下我们需要修改 UA  

![CG-8](https://github.com/Aniverse/WiKi/raw/master/Images/RSS/How.to.RSS-CG-8.png)  

复制下来的格式形如：`__cfduid=abcd123456789; uid=12450; pass=123sometimesnaive` 就没问题了




# 3. 配置 RSS

Flexget 和 ruTorrent 的入门级 RSS 配置我先略过了，我这里就先说需要 Cookies 和 url_rewrite 的情况  

## Flexget RSS

先是 Flexget 的模板，直接上配置文件：  

```YAML
tasks:
  AsianDVDClub:
    rss: http://asiandvdclub.org/rss.xml
    headers:
      Cookie:"__cfduid=abcd123456789; uid=123456; pass=123sometimesnaive; punbb_cookie=a%abcd123456789; PHPSESSID=abcd123456789"
    urlrewrite:
      sitename:
        regexp: 'http://asiandvdclub.org/details.php\?id=(?P<id>\d+)'
        format: 'http://asiandvdclub.org/download.php?id=\g<id>'
    accept_all: yes
    download: /home/aniverse/deluge/watch
  Cinematik:
    rss: https://www.cinematik.net/rss.php?key=JzKZN8V88gmSw43B&which=3
    headers:
      Cookie: "__cfduid=abcd123456789; xuid=123456; xpass=123sometimesnaive; PHPSESSID=abcd123456789"
    accept_all: yes
    download: /home/aniverse/deluge/watch
  CinemaGeddon:
    rss: http://cinemageddon.net/rss.xml
    headers:
      Cookie: "__cfduid=abcd123456789; uid=12450; pass=123sometimesnaive"
    accept_all: yes
    download: /home/aniverse/deluge/watch
```

简单地讲解下：

**[headers](https://flexget.com/Plugins/headers)**：这个插件可以修改 request headers（请求头）。刚才在获取 Cookies 那一章里提到过这个东西，这个插件改的就是这个。一般让 headers 里带上 cookies 就行（有些情况下可能还需要修改 User-Agent）  
PS：也可以用 Flexget 的 [Cookies](https://flexget.com/Plugins/cookies) 来搞定 cookies，不过我觉得还是用 headers 更方便  

另外实测 `__cfduid` 和 `PHPSESSID` 其实不写也没事，不过既然都复制下来了，写上去也无妨……

**[urlrewrite](https://flexget.com/Plugins/urlrewrite)**：对 RSS 源里给出的网址进行替换。将原本形如 `http://asiandvdclub.org/details.php?id=123456` 的种子描述页面链接替换为形如 `http://asiandvdclub.org/download.php?id=123456` 的种子下载链接

你可能会有一些疑问：  

【1】CinemaGeddon 的 RSS 下载链接其实是要替换的，为什么没配置 urlrewrite？  

这是因为，Flexget 自带的 **[URL Rewriters](https://flexget.com/URLRewriters)** 模板中已经包含了 CinemaGeddon 的下载链接替换模板，都不需要我自己来写了。  
但是也有个蛋疼的问题，Flexget 对于特殊字符的 urlrewrite 存在问题，导致下载形如 `Los Días Calientes [Argentina] [1966/WEB-DL/x264] (Comedy)` 的种子的时候会失败，这种时候如果能不用自带的模板下载种子的话反而能避开这个问题  
这个问题我暂时还没研究如何解决，要么去给官方反应问题等待官方修复，要么自己把这个插件禁用掉（我也还没试过怎么禁用）  

【2】Cinematik 的 RSS 链接里带了 key，为什么还需要 Cookies？  

Tik 真的是蛋疼，查看源码后你会看到它有三种 RSS 链接  

![TIK-1](https://github.com/Aniverse/WiKi/raw/master/Images/RSS/How.to.RSS-TIK-1.png)  

我第一反应就是，这个 `direct download` 应该就是可以直接下载且带 passkey 的（链接里都写着 key 了）——但实际上并不是。打开链接后打开这个 RSS 链接后你会发现，这个 RSS 源确实给了你下载链接，不需要你 rewrite url 了，但是下载链接不带 passkey，你还是需要配置 cookies  

![TIK-2](https://github.com/Aniverse/WiKi/raw/master/Images/RSS/How.to.RSS-TIK-2.png)  

此外这个 RSS 源里还有一个不带 key 的 direct download RSS 链接，效果和带 key 的是一样的：  
`https://www.cinematik.net/rsstik-direct.xml`  
然而这个链接你在 Tik 种子页面的源码里是找不到的……  






## ruTorrent RSS

ruTorrent 不仅支持正则，还支持 url_rewrite 和 cookies，也足够满足大多数情况下的 RSS 需求了。  


### ruTorrent RSS min Interval

先说个设置方面的问题，可能不少人都发现了，ruTorrent RSS 的间隔似乎不能设定到 2 分钟以内，这对于某些需要争分夺秒却又没有 AutoDL-Irssi 用的刷流环境并不合适。实际上这是 ruTorrent RSS 插件自带的一个限制，[代码见此](https://github.com/Novik/ruTorrent/blob/master/plugins/rss/conf.php#L7)  

这个限值无法在 ruTorrent 上修改，需要修改 `ruTorrent路径/plugins/rss/conf.php`，下边列出一些路径供参考：  

[rtinst](https://github.com/arakasi72/rtinst) 脚本（[inexistence](https://github.com/Aniverse/inexistence) 用的也是 [rtinst](https://github.com/Aniverse/rtinst)）安装的 ruTorrent，这个路径是  
`/var/www/rutorrent/plugins/rss/conf.php`  
[QuickBox](https://github.com/QuickBox/QB) 脚本  
`/srv/rutorrent/plugins/rss/conf.php`  
Feral Hosting  
`~/www/你的用户名.机器名/public_html/rutorrent/plugins/rss/conf.php`  
Pulsed Media  
`~/www/rutorrent/plugins/rss/conf.php`  
Seedboxes.cc（这家直接帮你改成 1 分钟了，都用不着你自己改）  
`/home/user/.www/rutorrent/plugins/rss/conf.php`  

至于 SeedHost／UltraSeedBox 等盒子，我现在没机器没法找，反正也在 www 目录下，不难找；其他脚本装的也同理  

文件找到以后，用这行命令修改  
`sed -i "s/\$minInterval = .*\;/\$minInterval = 1\;/" conf.php_的路径`  

什么？1 分钟你还嫌不够快？那你自己改代码吧……  
**警告**：RSS 频率太高可能会导致被判定为 ddos 或恶意 RSS，轻则 ban 盒子 IP，重则 ban 号（也可能什么也不会发生……）  



### ruTorrent Cookies

ruTorrent 通用的 Cookies 在设置里：  

![ruTorrent-RSS-Cookies-1](https://github.com/Aniverse/WiKi/raw/master/Images/RSS/ruTorrent-RSS-Cookies-1.png)  

```
asiandvdclub.org|uid=654321;pass=2young2simple;
cinematik.net|xuid=12345;xpass=s0met1mesna1ve;
```
然后你加种时直接用类似 `https://asiandvdclub.org/download.php?id=117677` 的链接就能直接添加到 rTorrent 上了  

不过似乎这个 Cookies 对 RSS 无效，对于需要 Cookies 的 RSS 源，你应该这么填写 Cookies：  

![ruTorrent-RSS-Cookies-2](https://github.com/Aniverse/WiKi/raw/master/Images/RSS/ruTorrent-RSS-Cookies-2.png)  

```
http://cinemageddon.net/rss.xml:COOKIE:uid=20020228;pass=tungcheehwa
https://www.cinematik.net/rsstik-direct.xml:COOKIE:xuid=20020228;xpass=tungcheehwa
```

### ruTorrent RSS-Url-Rewrite

配置完 Cookies 后你会发现有些站点已经可以下载了（比如 RacingForMe，Cinematik），有些站点还是无法下载，这是因为报道上出现了偏差，这时候就需要 `rssurlrewrite` 了  
首先，随便选种一个 RSS 到的项目，右键——规则管理：

![ruTorrent-urlrewrite-1.png](https://github.com/Aniverse/WiKi/raw/master/Images/RSS/ruTorrent-urlrewrite-1.png)  

按照我图中的设置操作：

![ruTorrent-urlrewrite-3.png](https://github.com/Aniverse/WiKi/raw/master/Images/RSS/ruTorrent-urlrewrite-3.png)  
![ruTorrent-urlrewrite-2.png](https://github.com/Aniverse/WiKi/raw/master/Images/RSS/ruTorrent-urlrewrite-2.png)  

```
|http://cinemageddon.net/details.php?id=(\d+)|i
http://cinemageddon.net/download.php?id=/${1}&name=${1}.torrent

|http://asiandvdclub.org/details.php\?id=(\d+)|i
http://asiandvdclub.org/download.php?id=${1}
```

在规则调试的测试中输入 RSS 源中的 URL，按下 `?` 按钮测试规则是否能正常执行  

至于其他站点的规则要怎么写，举一反三吧  

### temp end

先写到这里了，剩下的以后有心情再写  




## To Do List

以下内容无限期 coming sooooooooon，并且随时可能弃坑：  

1. ruTorrent 正则的简单用法（体积过滤等）（其实已经有很多现成的英文教程）  
2. ruTorrent RSS 入门级教程（其实大多数人都会）  
3. Flexget RSS 入门级教程（已经烂大街，我也在配置文件模板里写过）  
4. qBittorrent RSS 入门级教程（不用教也会系列）  
5. Deluge YaRSS2 RSS 入门级教程  
6. Flood RSS 入门级教程  

















