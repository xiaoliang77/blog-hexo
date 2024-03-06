---
title: 【js脚本】Flex 3 补丁管理 更新 1.6
layout: post
categories: [脚本]  #分类
tag: [js脚本,Flex,补丁] #标签
date: 2020-06-15
cover: https://blog-github-img.87xl.cn/img/js-flex3/0.png
---
![](https://blog-github-img.87xl.cn/img/js-flex3/0.png)

<!-- more -->

**更新内容**
======
> 2020年6月15日 更新：
> 修复：分享最后一个补丁节点对齐问题。
> 修复：修复原先补丁分割造成补丁无法显示问题。
> 新增：文件分享面板添加管理补丁。直接Filza文件内操作，无需借助iCloud云盘。
> 新增：补丁数量显示。
> 新增：关闭按钮。
> 去除：补丁分享名称自动添加"_patches"。

> 2020年6月9日 更新：
> 修复：列表排序错乱问题。
> 修复：ios13系统分享单个补丁名字错乱问题。
> 新增：云端补丁下载进度条。

> 2019-11-21 更新　
> 修复：部分补丁无法添加问题。

> 2019-3-11 更新
> 新增：云端补丁搜索功能。

> 2019-3-4 更新
> 新增：单个补丁分享功能。
> 新增：查看补丁详细功能。
> 修复：清空补丁后重新运行插件还有的问题。

**使用前言**
======
> 这里的js脚本是指，运行在 [jsbox](https://itunes.apple.com/cn/app/jsbox-%E5%AD%A6%E4%B9%A0%E5%86%99%E4%BB%A3%E7%A0%81/id1312014438?mt=8) 软件上的 **JavaScript** 脚本程序。安装脚本前首先你的手机必须有安装这个App。
> 　
> 没有安装的请到（[App Store](https://itunes.apple.com/cn/app/jsbox-%E5%AD%A6%E4%B9%A0%E5%86%99%E4%BB%A3%E7%A0%81/id1312014438?mt=8)）苹果商店搜索安装。

**脚本介绍**
======

> 该脚本可以方便的管理和获取一些补丁
> 单个补丁分享功能,查看补丁详细功能.
> 也可以合成 Flex 多个 patches.plist 文件
> 内置云端补丁，补丁由网友分享和 Flex 插件内置补丁，最后由小良整理上传。（ps：如果你有好用的补丁而且愿意分享的话，可以联系我）

**使用说明**
======

> 1、用 [Filza]() 文件管理器 找到 [Flex 3]() 补丁文件（路径：[/var/mobile/Library/Application Support/Flex3]()）把 [patches.plist]() 文件导出到 [iCloud 云盘中]()（也可复制[patches.plist]()文件内源码）。
> 　
> 2、打开 [JSBox]() 运行 [Flex 3补丁管理]() 这个脚本，添加补丁，以[iCloud 云盘]() 或 [剪切板]() 方式添加（当然也可以直接从脚本云端添加）
> 　
> 3、完成后就可以导出文件放到 [Flex 3]() 补丁文件 替换原先的就可以使用了。
> 　
> 如果上面文字看得不是很懂请看下面视频教程。

**视频演示一**
======
> <video id="video" controls="" preload="none" width= "100%" poster="https://blog-github-img.87xl.cn/img/js-flex3/0.png">
      <source id="mp4" src="https://u.nu/udio8" type="video/mp4">
</video>
> 　
> 视频地址：https://u.nu/udio8

**视频演示二**
======
> <video id="video" controls="" preload="none" width= "100%" poster="https://blog-github-img.87xl.cn/img/js-flex3/0.png">
      <source id="mp4" src="http://t.cn/EIcPhm3" type="video/mp4">
</video>
> 　
> 视频地址：http://t.cn/EIcPhm3

**脚本预览**
======
> ![](https://blog-github-img.87xl.cn/img/js-flex3/1.png)
> ![](https://blog-github-img.87xl.cn/img/js-flex3/2.png)
> ![](https://blog-github-img.87xl.cn/img/js-flex3/3.png)

**脚本安装**
======
> 直链安装：
> https://ae85.cn/jsbox/flex3.html
> 　
> js版或wf版【[ 小良 - 更新器](/js-gxq.html) 】 均可获取安装。
> > 注：如果添加不了，请使用复制代码的方式添加。请参考下面文章：
> > [关于JSBox无法安装脚本的解决方法](https://mp.weixin.qq.com/s/9E86yTg1Nwm7XuZeOqhVLQ)

> 最后在说下如果你有好用的插件而且愿意分享的话，请联系我或直接将patches.plist 文件发我邮箱上（84088289@qq.com） 