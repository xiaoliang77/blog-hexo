---
title: 使用Serv00免费虚拟主机部署Alist
layout: post
categories: [pc]  #分类
tag: [alist,虚拟主机] #标签
date: 2024-03-19
cover: https://blog-github-img.87xl.cn/img/picgo/202404130839579.png
---

![](https://blog-github-img.87xl.cn/img/picgo/202404130839579.png)

<!-- more -->
[Serv00](https://www.serv00.com/)是一个提供**免费**的Virtual Host的平台，其托管平台使用的是**FreeBSD**系统，并**不是Linux**。每个账号有效期**10年**，超过**三个月**不登入Panel以及SSH则会被删除账号。

其提供的服务大致如下表所示：

| 名称 | Serv00 免费提供 |
| --- | --- |
| 存储空间 | 3 GB |
| 每月流量 | unlimited |
| 网站数量 | 100 |
| MySQL | 10 |
| PostgreSQL | 3 |
| MongoDB | 3 |
| GIT/SVN/HG 仓库 | 3 |
| TCP/UDP端口 | 3 |
| PHP解释器 | 3 |
| 系统进程 | 15 |
| RAM | 512MB |
| 备份 | 7天 |
| 服务器放置 | 欧盟 |
| 免费子域名 | [http://login.serv00.net](http://login.serv00.net/) |
| 技术支持 | 只有论坛 |
| SLA | 不支持 |
| 现代技术 | 支持 |
| SSH访问 | 支持 |
| SSH隧道 | 不支持 |
| 远程数据库访问 | 不支持 |
| 固态硬盘 | 支持 |
| 没有广告 | 支持 |
| 价格 | 免费 |

> 更详细的配置说明请查阅官方说明。

Serv00使用的面板是这种共享虚拟主机常用的DevilWEB，还挺好上手的。下面详细介绍一下使用Serv00部署Alist的方法步骤：

> **觉得一步步手动操作太麻烦的，可以直接翻到最末，提供了我的blog地址，提供了一些简化操作的一键式命令。**

## 注册账号

首先去serv00的官网[注册一个账号](https://www.serv00.com/offer/create_new_account)，最好**不要使用国内邮箱**，注册信息请尽可能**真实填写**。

![](https://pic1.zhimg.com/v2-0f3b0d1861e310f672a9f228de6d16cc_b.jpg)

注册账号

接着你可以在邮箱里收到你的注册信息的邮件：

![](https://pic2.zhimg.com/v2-29b69c403e9bb492ea1e75dad8cc6aa5_b.jpg)

注册邮件

邮件最末有Panel的入口地址和[文档链接](https://docs.serv00.com/)以及[论坛链接](https://forum.serv00.com/)，接下来登入Panel进行操作：

![](https://pic4.zhimg.com/v2-a3ae7c972a622d7ab3b137f7f0eb7243_b.jpg)

DevilWEB

首先去左侧的**Additional Service**选项卡中，找到**Run your own applications**选项，将其设置为允许：

![](https://pic1.zhimg.com/v2-494fc0693210873b8a122e3e33403be4_b.jpg)

运行自己的应用

接着去**Port reservation**选项卡，使用**Add port**功能，随机添加一个**TCP端口**：

![](https://pic1.zhimg.com/v2-8b0cca6d0ff3e209e7b1780205cc6b50_b.jpg)

添加端口

记下你添加的端口，后面要用。

接着使用SSH登入到你的账户，我使用的SSH客户端是[Termius](https://termius.com/)：

![](https://pic1.zhimg.com/v2-da4ba766ecd2b3a96aa7d5d5b9d6cb28_b.jpg)

登入成功！

> 注意，这一步可能你的网络不一定连得上，可能需要使用打倒美帝的上网手段。

## 部署Alist

[Alist的官方仓库](https://github.com/alist-org/alist)并没有提供FreeBSD版本的可执行文件构筑，但是我在Github上找到了Unofficial的，专门为Alist构筑FreeBSD版本的[仓库](https://github.com/uubulb/alist-freebsd)，所以只要使用这个仓库就可以在Serv00上部署使用Alist了。

Serv00本身提供的网站托管在`~/domains`路径下，所以我建议把Alist也部署到这个路径下的子目录：

```bash
mkdir -p ~/domains/alist && cd ~/domains/alist 
```

接着下载目前`uubulb/alist-freebsd`提供的最新版的Alist的可执行二进制文件构筑：

```bash
wget https://github.com/uubulb/alist-freebsd/releases/download/v3.30.0/alist && chmod +x alist
```

然后需要先启动一次Alist以生成配置文件，此次启动一定会失败，请不用在意：

接着回到Panel中，找到MySQL选项卡，使用Add database功能新建一个数据库：

![](https://pic2.zhimg.com/v2-f6b1c1086558dab0fdcb382180438599_b.jpg)

创建数据库

> 密码要求含有大写字母、小写字母和数字三种字符，且长度必须超过6个字符。

接下来进入File manager选项卡，进入`~/domains/alist/data`路径，可以看到一个名为`config.json`的文件，右键点击，选择View/Edit > Source Editor，进行编辑：

![](https://pic3.zhimg.com/v2-428d35264f44fe6b12152658813114d6_b.jpg)

我主要修改了CDN、database、scheme三个部分，其中CDN可以在[Alist的官方文档](https://alist.nn.ci/zh/config/configuration.html#cdn)找到，请选择你本地网络连接速度最快的一个。

scheme部分，我选择修改adress为`127.0.0.1`本地回环，是为了避免被他人使用`http://ip:port` 的方式进行访问。至于自己怎么访问，我在本文后面的部分会进行介绍。port要改成自己前面放行的端口。

database部分，type需要改成\`mysql\`，host填写你在注册邮件中看到的mysql的地址，port是默认的3306，用户名、密码、数据库名则按照你创建的情况进行填写。

改完之后，点击save保存，接着回到SSH窗口中进行操作。

先启动一次，查看运行是否正常：

![](https://pic3.zhimg.com/v2-722472003c13bc70e85ad58d7902038a_b.jpg)

运行正常，记得把管理员用户的密码记住。接着使用`Ctrl+c`停止运行。

## 绑定域名

此时还没有访问Alist的方法，因为监听的地址是本地回环，所以需要将其反向代理出来。我选择使用Cloudflare提供的Argo通道，顺带给Alist绑定自己的域名。

Cloudflared官方仓库没有提供FreeBSD平台的客户端，但是和Alist一样的，我找到了Unofficial的FreeBSD版本的[构筑](https://cloudflared.bowring.uk/)，接下来使用它打隧道：

新建并进入Cloudflared的工作目录：

```bash
mkdir -p ~/domains/cloudflared && cd ~/domains/cloudflared
```

下载Cloudflared：

```bash
wget https://cloudflared.bowring.uk/binaries/cloudflared-freebsd-2023.10.0.7z && 7z x cloudflared-freebsd-2023.10.0.7z && rm cloudflared-freebsd-2023.10.0.7z && mv -f ./temp/cloudflared-freebsd-2023.10.0 ./cloudflared && rm -rf temp
```

然后在[Cloudflare的面板](https://one.dash.cloudflare.com/)中，找到Networks分类下的Tunnels功能，点击Create a tunnel，选择Cloudflared，Next，随便取个名字，Next，往下翻，可以看到Run the following command，然后给了一串命令，将其复制出来，大概是这样的：

```powershell
cloudflared.exe service install eyJhIjoiNzh...............V5TWpBeSJ9
```

前面的不需要管，只需要保留最后ey开头的那串很长的TOKEN，去SSH中测试运行Cloudflared：

```bash
./cloudflared tunnel --edge-ip-version auto --protocol http2 --heartbeat-interval 10s run --token eyJhIjoiNzh...............V5TWpBeSJ9
```

> 记得把最后的那一串替换成你的TOKEN。

接着回到Cloudflare的面板，继续点击Next，然后添加一个自己的域名，Service中，Type选择HTTP，URL填写localhost:PORT，其中PORT为你的Alist对应的端口。点击Save Tunnel后，可以看到自己新建的Tunnel上线。

接着使用`Ctrl+c`停止运行。然后安装进程管理工具pm2：

```bash
bash <(curl -s https://raw.githubusercontent.com/k0baya/alist_repl/main/serv00/install-pm2.sh)
```

然后使用pm2启动Cloudflared：

```text
~/.npm-global/bin/pm2 start ./cloudflared -- tunnel --edge-ip-version auto --protocol http2 --heartbeat-interval 10s run --token eyJhIjoiNzh...............V5TWpBeSJ9
```

> 记得把最后的那一串替换成你的TOKEN。

再启动Alist：

```text
cd ~/domains/alist && ~/.npm-global/bin/pm2 start ./alist -- server
```

到这里，就可以直接通过你的域名访问刚刚部署的Alist了。

## 收尾工作

听说Serv00会不定时重启机器，所以我们把pm2添加开机自启，可以保证每次重启都能由pm2调动Alist和Cloudflared。而且Serv00每三个月内必须要有一次登录面板或者SSH连接，不然会删号，也可以通过一个脚本解决问题，接下来我会详细说明。

### 自动定时SSH

在Panel中找到File manager选项卡，进入alist所在的路径，然后找到上方Send按钮左边的+，选择New empty file，文件名命名为`auto-renew.sh`， 右键点击`auto-renew.sh`，选择View/Edit > Source Editor，进行编辑，把下面的代码块的内容都复制进去：

```bash
#!/bin/bash

while true; do
  sshpass -p '密码' ssh -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null -tt 用户名@地址 "exit" &
  sleep 259200  #30天为259200秒
done
```

> 记得把其中的密码、用户名、ssh的地址修改为你自己的。

保存后回到SSH中，进入`auto-renew.sh` 所在的路径，并使用pm2管理运行它：

```bash
cd  ~/domains/alist && chmod +x auto-renew.sh && ~/.npm-global/bin/pm2 start ./auto-renew.sh
```

这样就会每隔一个月自动执行一次SSH连接，自己SSH自己进行续期。

### 添加开机自启

在Panel中找到Cron jobs选项卡，使用Add cron job功能添加任务：

![](https://pic2.zhimg.com/v2-8aef51a10357b6c41bab39cee776a0bd_b.jpg)

Specify time选择After reboot，即为重启后运行。Form type选择Advanced，Command写：

```bash
/home/你的用户名/.npm-global/bin/pm2 resurrect
```

> 记得把你的用户名改为你的用户名

添加完之后，在SSH窗口保存pm2的当前任务列表快照：

```bash
~/.npm-global/bin/pm2 save
```

这样每次serv00不定时重启任务时，都能自动调用pm2读取保存的任务列表快照，恢复任务列表。

以上就是Serv00搭建使用Alist的全部过程。如果你觉得这样一步一步手动部署太繁琐，你可以参照我的blog，有更轻松的部署办法：[Saika's Blog](https://blog.rappit.site/)


文章转载自：[知乎](https://zhuanlan.zhihu.com/p/680607217)