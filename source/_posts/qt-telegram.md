---
title: Telegram - 电报 (TG,纸飞机) | 新手指南
layout: post
categories: [其他]  #分类
tag: [电报,TG,Telegram] #标签
date: 2020-07-26
cover: https://blog-github-img.87xl.cn/img/qt-telegram/0.png
---

![](https://blog-github-img.87xl.cn/img/qt-telegram/0.png)

<!-- more -->
> “ Telegram在中国也叫电报简称TG，是个国外的聊天工具，提供频道、群组、机器人等功能。”
**前言**
======
Telegram 是一款开源且跨平台的 IM 工具，类似国内的微信。不同的是Telegram 使用的是自己开发的MTProto协议加密通讯。这里我就不过多说介绍这些理论东西了，关于Telegram更多详细介绍可以自己网上搜索相关资料，这里我们自己进入主题。

**下载 Telegram**
======
直接在苹果商店 App Store 搜索下载安装即可。

![](https://blog-github-img.87xl.cn/img/qt-telegram/1.jpg)


**使用 Telegram**
======
Telegram是相当好的一款通讯工具，不过在天朝是难以访问，需要借助科学上网去突破。如果您有科学上网的方式可以略过此步。

> ①、使用TG软件内置代理功能连接，打开 https://ae85.cn/ 链接到Safari浏览器中打开，下滑找到Telegram 直连这个 点击进去。（ps：此代理是第三方代理，使用此方法会出现第三方广告群组）
> 　
> ![](https://blog-github-img.87xl.cn/img/qt-telegram/2.png)

> ②、使用第三方科学上网工具，工具这里就不说了，如果您有s s连接工具恰好又没有节点，这里我提供一个免费节点的获取JSBox脚本，https://87xl.cn/free-ss.html 


**Telegram 设置中文**
======
> ①、点击：[tg://setlanguage?lang=classic-zh-cn](tg://setlanguage?lang=classic-zh-cn) 或者这条链接在浏览器中打开，跳转到TG选择 Change 就可以了。
> 　
> ![](https://blog-github-img.87xl.cn/img/qt-telegram/3.jpg)

> ②、直接到TG搜索：@zh_cn  找到提供中文语音包的群组进去找对应的语音包安装即可。

**Telegram 关闭敏感模式**
======
由于ios某些原因要求限制在苹果设备上的社交 App 中的敏感内容，这就导致有些有敏感内容的群组/频道是无法进入查看消息，后来Telegram 官方终于也针对ios这个限制做出解决方案，提供了类似的关闭敏感内容过滤的开关。

> 1.打开 https://web.telegram.org/ 链接，登录你需要关闭敏感内容过滤的TG账号
> 2.打开 Settings - Show Sensitive Content
> 3.打开  Disable filtering 开关
> 4.关闭 Telegram iOS 端，重新打开，你将看到原本被过滤的群组已经可以正常进入了
> 　
> ![](https://blog-github-img.87xl.cn/img/qt-telegram/4.png)

**Telegram 机器人（bot）**
======
Bot 的机制体现了 Telegram 开放的特性，大大丰富了 Telegram 的用法。比如通过 bot 来 RSS 订阅新闻或博客，发到群组里；还可以帮助管理群组，可以提供翻译，可以代下文件，可以提醒网站更新等。这里推荐一些bot

> [@hao1234bot](https://t.me/hao1234bot) 【超级索引】：Telegram上的Hao123

> [@haoyybot](https://t.me/haoyybot) 【好音乐搜索】：下载音乐

> [@RSSWBot](https://t.me/RSSWBot) 【RSS屋】：提供全文RSS订阅源

> [@kaiche123bot](https://t.me/kaiche123bot) 【开che机器人】：命令/kc

> [@kaiche888_bot](https://t.me/kaiche888_bot) 【老司机kai车】：随机命令/stochastic

> [@getmediabot](https://t.me/getmediabot)【下载机器人】：可下载youtube,twitter等网站视频

> [@xiannvgong_bot](https://t.me/xiannvgong_bot)【仙女宫】：套图发布机器人命令/hello 随机9张，/all 随机一整套。

> [@GetPublicLinkBot](https://t.me/GetPublicLinkBot)【TG文件外链】：将telegram文件转发给这个bot，它会生成外部下载链接让你可以用第三方下载工具（例如idm，迅雷等）下载，或者转存到你的GOOGLE云盘（需要先进行绑定）


**Telegram 语音转MP3**
======
TG原语音的格式是ogg格式，导出是无法播放的，需要转换成MP3格式才可以在其他地方播放，这里小良做了一个js脚本来实现TG语音转成mp3格式。

> 脚本演示视频：https://u.nu/xsy79
> 　
> <video id="video" controls="" preload="none" width= "100%" poster="https://blog-github-img.87xl.cn/img/qt-telegram/0.png">
      <source id="mp4" src="https://u.nu/xsy79" type="video/mp4">
</video>
> 　
> 脚本安装：https://ae85.cn/jsbox/tgzmp3.html