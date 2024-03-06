---
title: 黑科技 | 让你的App证书永不过期的方法（无需任何插件）
layout: post
categories: [其他]  #分类
tag: [教程,越狱,证书] #标签
date: 1554134400000
cover: https://blog-github-img.87xl.cn/img/qt-appzs/0.png
---

![](https://blog-github-img.87xl.cn/img/qt-appzs/0.png)

<!-- more -->

> **在苹果公司对App企业版证书监管力度越来越大的的同时，带给我们玩家的是一种多么痛苦的事，原本安装的App没两天证书就又掉了，导致App无法使用，里面的东西也不好拿出来。最近我也看到群里有小伙伴讨论证书续签的问题，很多朋友都是安装签名插件之类的。今天小良就来教大家一种方法，无需任何插件就能解决这种困境。**

**前言：**
======
> 首先说明下，这个方法是需要手机 <font color=#f40>越狱</font> 并有安装 <font color=#f40>文件管理器</font> ，建议使用 <font color=#f40>Filza</font> 这个文件管理器。
> 　
> 在有些特殊的App不能上架 App Store 商店，或者在苹果公司审核不过的App要想给别人使用，那就得给App签上企业证书，或者个人证书。然后苹果公司对证书这块有时候也会比较严，时不时封杀一批证书。导致我们安装好的App隔三差五的用不了，又要重新安装。最致命的还是App内的有些质料确是拿不出来。
> 　
> 相信很多越狱的朋友都会安装(<font color=#f40>ReProvision</font>)这么一个签名续签的一个插件，<font color=#f40>其实完全不用安装这个插件。</font>
> 　
> 今天教大家的方法其实很简单：就是<font color=#f40>删除证书大法</font>

**图文教程：**
======
> 第一步：安装好App后，当你打开app时会提示 <font color=#f40>“未受信任········” </font>。这个时候不要慌。
> ![](https://blog-github-img.87xl.cn/img/qt-appzs/1.png)
> 　
> 第二步：打开 <font color=#f40>Filza</font> 这个文件管理器，进入证书目录：<font color=#f40>/var/MobileDevice/ProvisioningProfiles</font>  以【<font color=#f40>时间</font>】方式排序，找到刚刚安装app时所生成的证书，向左滑动【<font color=#f40>删除</font>】证书。
> ![](https://blog-github-img.87xl.cn/img/qt-appzs/2.png)
> 　
> 第三步：【<font color=#f40>注销</font>】你的手机。然后再去打开你刚刚安装的app就可以正常使用了。
> > <font color=#f40>注意：此方法需要你手机是保持在越狱状态，否则App是无法正常使用的。还有就是越狱工具的证书不要删除了。</font>

**视频教程：**
======
> <video id="video" controls="" preload="none" width= "100%" poster="https://blog-github-img.87xl.cn/img/qt-appzs/0.png">
      <source id="mp4" src="http://t.cn/EiXGSbX" type="video/mp4">
</video>
> 　
> 视频地址：http://t.cn/EiXGSbX
