---
title: GoIndex - 无服务器架构 Google Drive 目录索引程序
layout: post
categories: [pc]  #分类
tag: [网盘,cloudflare,谷歌] #标签
date: 2018-02-1
cover: https://blog-github-img.87xl.cn/img/pc-goindex/0.jpg
---

![](https://blog-github-img.87xl.cn/img/pc-goindex/0.jpg)

<!-- more -->
**前言**
======
GoIn­dex 全称 Google Drive Di­rec­tory In­dex，它是一款可以部署在 Cloud­flare Work­ers 上的无服务器架构 (Server­less) Google Drive 目录索引程序，它可以将 Google Drive 文件以目录形式列出，并且可以通过直链进行下载，如果视频是 MP4 格式还可以在线观看。由于流量是通过 Cloud­flare 中转，所以即使在被限制的网络环境下也能自由的使用。本篇教程讲解的是 GoIn­dex 使用自定义 API 部署的过程，理论上更安全且下载速度更快。

**准备工作**
======
* Google 账号
* CloudFlare 账号
* GoIndex 源码

打开 index.js 可以看到一些可以自由修改的参数。其中最后四项是需要我们手动去获取的参数。

```bash
"siteName": "GoIndex", // 网站名称
"root_pass": "index",  // 根目录密码，优先于.password
"version" : "1.0.6", // 程序版本
"theme" : "material", // material  classic
"client_id": "",
"client_secret": "",
"refresh_token": "", // 授权 token
"root": "root" // 根目录ID
```
**获取 client_id 与 client_secret**
======
> NOTICE: 部分教育邮箱可能无法开启 API ，这是因为管理员没有开放权限，你可以使用自己的账号去创建 API 。

* [启用 Google Drive API](https://console.cloud.google.com/apis/api/drive.googleapis.com/overview)
![](https://blog-github-img.87xl.cn/img/pc-goindex/1.png)

* [创建 OAuth client ID](https://console.cloud.google.com/apis/credentials/oauthclient)，首次创建会让你配置同意屏幕，填写应用名称后直接保存即可。
![](https://blog-github-img.87xl.cn/img/pc-goindex/2.png)

* 应用类型选择其他，名称随意。
![](https://blog-github-img.87xl.cn/img/pc-goindex/3.png)

* 然后就可以看到客户端ID（client_id）和客户端密钥（client_secret），复制并保存好。
![](https://blog-github-img.87xl.cn/img/pc-goindex/4.png)

**获取 refresh_token**
======
* 安装 Rclone

```bash
curl https://rclone.org/install.sh | bash
```
* 输入rclone config命令，会出现以下信息，参照下面的注释进行操作。

```bash
$ rclone config
...
e) Edit existing remote
n) New remote
d) Delete remote
r) Rename remote
c) Copy remote
s) Set configuration password
q) Quit config
e/n/d/r/c/s/q> n  # 选择n，新建
name> gd
Type of storage to configure.
Enter a string value. Press Enter for the default ("").
Choose a number from below, or type in your own value
 1 / 1Fichier
   \ "fichier"
 2 / Alias for an existing remote
   \ "alias"
 3 / Amazon Drive
   \ "amazon cloud drive"
 4 / Amazon S3 Compliant Storage Provider (AWS, Alibaba, Ceph, Digital Ocean, Dreamhost, IBM COS, Minio, etc)
   \ "s3"
 5 / Backblaze B2
   \ "b2"
 6 / Box
   \ "box"
 7 / Cache a remote
   \ "cache"
 8 / Citrix Sharefile
   \ "sharefile"
 9 / Dropbox
   \ "dropbox"
10 / Encrypt/Decrypt a remote
   \ "crypt"
11 / FTP Connection
   \ "ftp"
12 / Google Cloud Storage (this is not Google Drive)
   \ "google cloud storage"
13 / Google Drive
   \ "drive"
14 / Google Photos
   \ "google photos"
15 / Hubic
   \ "hubic"
16 / JottaCloud
   \ "jottacloud"
17 / Koofr
   \ "koofr"
18 / Local Disk
   \ "local"
19 / Mail.ru Cloud
   \ "mailru"
20 / Mega
   \ "mega"
21 / Microsoft Azure Blob Storage
   \ "azureblob"
22 / Microsoft OneDrive
   \ "onedrive"
23 / OpenDrive
   \ "opendrive"
24 / Openstack Swift (Rackspace Cloud Files, Memset Memstore, OVH)
   \ "swift"
25 / Pcloud
   \ "pcloud"
26 / Put.io
   \ "putio"
27 / QingCloud Object Storage
   \ "qingstor"
28 / SSH/SFTP Connection
   \ "sftp"
29 / Transparently chunk/split large files
   \ "chunker"
30 / Union merges the contents of several remotes
   \ "union"
31 / Webdav
   \ "webdav"
32 / Yandex Disk
   \ "yandex"
33 / http Connection
   \ "http"
34 / premiumize.me
   \ "premiumizeme"
Storage> 13      # 选择 13 / Google Drive
** See help for drive backend at: https://rclone.org/drive/ **

Google Application Client Id
Setting your own is recommended.
See https://rclone.org/drive/#making-your-own-client-id for how to create your own.
If you leave this blank, it will use an internal key which is low performance.
Enter a string value. Press Enter for the default ("").
client_id> # 输入 客户端ID
Google Application Client Secret
Setting your own is recommended.
Enter a string value. Press Enter for the default ("").
client_secret> # 输入 客户端密钥
Scope that rclone should use when requesting access from drive.
Enter a string value. Press Enter for the default ("").
Choose a number from below, or type in your own value
 1 / Full access all files, excluding Application Data Folder.
   \ "drive"
 2 / Read-only access to file metadata and file contents.
   \ "drive.readonly"
   / Access to files created by rclone only.
 3 | These are visible in the drive website.
   | File authorization is revoked when the user deauthorizes the app.
   \ "drive.file"
   / Allows read and write access to the Application Data folder.
 4 | This is not visible in the drive website.
   \ "drive.appfolder"
   / Allows read-only access to file metadata but
 5 | does not allow any access to read or download file content.
   \ "drive.metadata.readonly"
scope> 1 # 完整权限访问
ID of the root folder
Leave blank normally.

Fill in to access "Computers" folders (see docs), or for rclone to use
a non root folder as its starting point.

Note that if this is blank, the first time rclone runs it will fill it
in with the ID of the root folder.

Enter a string value. Press Enter for the default ("").
root_folder_id> # 留空，回车
Service Account Credentials JSON file path
Leave blank normally.
Needed only if you want use SA instead of interactive login.
Enter a string value. Press Enter for the default ("").
service_account_file> # 留空，回车
Edit advanced config? (y/n)
y) Yes
n) No
y/n> n
Remote config
Use auto config?
 * Say Y if not sure
 * Say N if you are working on a remote or headless machine
y) Yes
n) No
y/n> n # 输入 n
If your browser doesn't open automatically go to the following link: https://accounts.google.com/o/oauth2/XXXXXXX
Log in and authorize rclone for access # 复制上面的链接到浏览器中打开进行授权。
```

* 在浏览器中你可能会遇到下图的提示，这是因为 API 是我们自己创建的，并没有通过 Google 的验证。
![](https://blog-github-img.87xl.cn/img/pc-goindex/5.png)

```bash
Enter verification code> # 在这里输入网页上显示的验证码
Configure this as a team drive?
y) Yes
n) No
y/n> y # 如果是团队盘输入 y ，否则输入 n
Fetching team drive list...
Choose a number from below, or type in your own value
 1 / P3TERX
   \ "0ADPHQ2hJ-6ZkUk9PVA"
Enter a Team Drive ID> 1 # 检测到团队盘，这里输入 1
2019/11/06 21:44:27 ERROR : Failed saving config "team_drive" = "0ADPHQ2hJ-6ZkUk9PVA" in section "gd" of the config file: section 'gd' not found
--------------------
[gd]
type = drive
client_id = 217429025371-pfu4k1ko34p4hku860kuj5k5v038f1u4.apps.googleusercontent.com
client_secret = 2VxOZcsItLFB8htDXDn2zl_e
scope = drive
token = {"access_token":"XXXXX","token_type":"Bearer","refresh_token":"1//0eDO2FT","expiry":"2019-11-06T22:44:23.013869707+08:00"} # 保存其中的 refresh_token
team_drive = 0ADPHQ2hJ-6ZkUk9PVA
--------------------
y) Yes this is OK
e) Edit this remote
d) Delete this remote
y/e/d> y # 输入 y 确认
Current remotes:

Name                 Type
====                 ====
Onedrive             onedrive
gd                   drive

e) Edit existing remote
n) New remote
d) Delete remote
r) Rename remote
c) Copy remote
s) Set configuration password
q) Quit config
e/n/d/r/c/s/q> q # 输入 q 退出
```

**获取根目录ID（root）**
======
这里的根目录是指 GoIn­dex 显示的根目录，可以是你网盘中的任意目录。打开网盘定位到某个目录或共享目录，地址栏 URL 中最后面部分的代码就是目录 ID 了。如果是个人网盘参数留空则是网盘根目录。
![](https://blog-github-img.87xl.cn/img/pc-goindex/6.png)

**创建 Workers**
======
* 登录 Cloudflare，点击右侧的 Workers 。
![](https://blog-github-img.87xl.cn/img/pc-goindex/7.png)

* 新建一个 Work­ers 子域名
> TIPS：后续无法更改，所以不要乱填。
![](https://blog-github-img.87xl.cn/img/pc-goindex/8.png)

* 点击Create a Worker新建一个 Worker
![](https://blog-github-img.87xl.cn/img/pc-goindex/9.png)

* 清空输入框中的内容，把修改好的 GoIndex 代码并粘贴进去，然后可以在左上角双击修改域名，再点击Save and Deploy即可。
![](https://blog-github-img.87xl.cn/img/pc-goindex/10.png)

* 最后获取到的****.workers.dev就是你的 GoIndex 地址了。