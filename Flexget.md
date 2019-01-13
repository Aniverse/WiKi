# Flexget 入门级教程

注意：
1. 新手最好在 SSH 或者 WebUI 下编辑 Flexget 配置文件；在 Windows 下也不要用系统自带的记事本编辑，容易出错（换行问题之类的）  
2. Flexget 配置文件遵循 YAML 格式，请注意空格和缩进  
3. `inexistence` 脚本安装完后的 Flexget 后默认不启用 RSS 功能  

如果需要使用 RSS 功能，主要有两个办法（如何使用见后文）：
1. 使用 daemon 模式的 schedules
2. 使用 cron






## 配置文件讲解

```YAML
# 预设模板
templates:
# 剩余空间模板，当 path 对应的路径的剩余空间小于 space 规定的数值的时候停止 RSS 下载
  freespace:
    free_space:
      path: /home/SCRIPTUSERNAME
      space: 10240
# qb 的模板，之后写 qb 就是指把种子推送到 qb 进行下载；下面 tr de rt 也是如此
# 我脚本里账号密码都帮你写好了，除非你自己改了账号、密码或者端口，不然以下这些客户端设置不用修改
  qb:
    qbittorrent:
      path: /home/SCRIPTUSERNAME/qbittorrent/download/
      host: localhost
      port: 2017
      username: SCRIPTUSERNAME
      password: SCRIPTPASSWORD
  tr:
    transmission:
      path: /home/SCRIPTUSERNAME/transmission/download/
      host: localhost
      port: 9099
      username: SCRIPTUSERNAME
      password: SCRIPTPASSWORD
  de:
    deluge:
      path: /home/SCRIPTUSERNAME/deluge/download/
      host: localhost
      port: 58846
      username: SCRIPTUSERNAME
      password: SCRIPTPASSWORD
# 体积过滤模板，min 是符合条件的最小种子体积，max 是符合条件的最大种子体积，单位均为 MB
# strict 默认是 yes，表示在无法确定大小的情况下就不下载，这里把它改成 no 了
# 也就是说，这段 size 的意思是，只下载体积为 6000-666666 MB 的种子，其他不满足条件的种子不下载
  size:
    content_size:
      min: 6000
      max: 666666
      strict: no

# 任务
tasks:

# HDChina 是任务名称，不一定要和网站名称一样
  HDChina:
# RSS 地址请自己修改成你需要的地址
    rss: https://hdchina.org/torrentrss.php
# 关闭对于 ssl 的验证
    verify_ssl_certificates: no
# 如果种子标题中有 HDChina 或 HDCTV，那就执行下载
    if:
      - "'HDChina' in title and '1080p' in title": accept
      - "'HDCTV' in title": accept
# HDChina 这个 RSS 任务所调用的模板，这里用了剩余空间、体积过滤、qb下载 这三个模板
# 实现的效果即为：使用 qb 下载，只下载体积介于 6000MB-666666MB 的种子，剩余空间小于 10GB 时候停止 RSS
    template:
      - freespace
      - size
      - qb
# 添加到 qbittorrent 的时候，自动对 RSS 到的种子添加 HDChina 的标签
    qbittorrent:
      label: HDChina

  MTeam:
    rss: https://tp.m-team.cc/torrentrss.php
    verify_ssl_certificates: no
# 正则表达式；标题带 OneHD 的种子就下载（accept，接受），带 MTeamPAD 的就不下载（reject，拒绝）
    regexp:
      accept:
        - OneHD
      reject:
        - MTeamPAD
    template:
      - de
# 可以不使用模板的体积过滤，针对每个任务单独设置体积过滤
    content_size:
      min: 15000
      max: 100000
      strict: no
# 添加到 deluge 的时候，自动对 RSS 到的种子设置 12800KB/s 的上传速度限制
    deluge:
      maxupspeed: 12800.0

# Flexget WebUI 设定，可以不改
# base_url 是为了反代设置的，需要使用反代的话就取消这个的注释，然后在安装了 rTorrent 的情况下（不装 rt 的话没有 nginx），Flexget WebUI 地址就变成了 https://你盒子的 IP 地址/flexget
web_server:
  port: 6566
  web_ui: yes
# base_url: /flexget

# 这里关闭 RSS 功能，如何打开请看下文
schedules: no
```






## 测试

输入这一句命令测试：
```
flexget --test execute
```
如配置文件存在语法错误，会提示你在第几行有什么错误  
如果配置文件没问题的话则会测试执行，不会真的下种子，可以用来测试配置文件写得是否合乎预期  

第一次使用 RSS 的时候难免会下载到一些已经出种的老种，为了解决这个情况，第一次执行 flexget 的时候，可以用  
```
flexget execute --learn
```
这样子不会下载种子，但是会把这次 RSS 到的种子标记为已下载，这样之后就不会下到老种了  







## 开启 RSS 功能

### 方法 1 ：使用 schedules

tasks 处写要执行 RSS 的任务名称，`minutes: 3` 表示每隔 3 分钟执行一次上述任务  
可以针对不同的 tasks 采用不同的 RSS 周期  

```YAML
schedules:
  - tasks: [HDChina,TTG]
    interval:
      minutes: 3
  - tasks: [Gods]
    interval:
      minutes: 1
```

### 方法 2 ：使用 cron

使用 cron 的话，schedules 最好改成 no，正如脚本里默认的那样（`schedules: no`）  
首先在 SSH 输入 crontab -e，选择一个文本编辑器，默认的 nano 即可 （nano 使用教程：http://man.linuxde.net/nano）  
设置 2 分钟执行一次 RSS，就在文件里（写在哪个位置无所谓，顶部也行、底部也行）输入：

```
*/2 * * * * /usr/local/bin/flexget --cron execute
```

（这里的就是 2 分钟执行一次的意思）  
保存、退出，之后可以在 WebUI 中看 Log 来判断 Flexget 是否有在正常工作，或者在 SSH 中输入 `flexget status` 查看状态  

## 其他

以上两个办法都是最短 1 分钟执行 1 次 RSS，如果你想实现更高的频率得用别的办法，这里不作介绍了  

**提示**：一般情况下不建议 RSS 频率太高，一是因为 Flexget 本身执行过程中会消耗一些系统资源，频率太高可能服务器撑不住；二是因为 RSS 频率太高可能有些站点认为你是在做恶意攻击。至于多久一次算是频率太高，你自己看着办吧……  


