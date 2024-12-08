---
created: 2024-10-08
updated: 2024-12-08
share: true
title: 解决京东轻量云主机 Debian 12.5.0 镜像无法安装 1Panel 的问题
date: 2024-10-08
lastmod: 2024-10-08
tags:
  - 1Panel
categories:
  - 折腾
slug: jdcloud-1panel-error
---

>本文写于 2024 年 10 月 8 日，后续会将此问题报告给京东云客服，期待解决～

## 情况说明

自己一直在使用腾讯云。前几个月频繁看到京东云的小广告，了解了一下是价格是真香，于是 50 元/年入手了这台位于宿迁的 2H2G3M 的京东轻量云。

今天打算重装下系统，安装 1Panel 面板，选择了 Debian 12.5.0 镜像。

系统重装好后，输入 1Panel 在 Debian 上的一键安装命令后按提示继续，最终出现报错：

```bash
E: The repository 'cdrom://[Debian GNU/Linux 12.5.0 _Bookworm_ - Official amd64 DVD Binary-1 with firmware 20240210-11:28] bookworm Release' does not have a Release file.
E: The repository 'http://mirrors.jdcloudcs.com/debian bookworm Release' no longer has a Release file.
E: The repository 'http://mirrors.jdcloudcs.com/debian-security bookworm-security Release' no longer has a Release file.
E: The repository 'http://mirrors.jdcloudcs.com/debian bookworm-updates Release' no longer has a Release file.
[1Panel Log]: docker 安装失败
您可以尝试使用离线包进行安装，具体安装步骤请参考以下链接：https://1panel.cn/docs/installation/package_installation/ 
```

最终导致无法安装 1Panel 面板。

## 尝试解决

作为技术小白，很庆幸现在 AI 技术的发达，于是向 AI 发起求助。

AI 告诉我使用命令 `nano /etc/apt/sources.list` 编辑软件源列表，将上面的 `cdrom` 行注释掉，再将下面三行的的京东云的源换成阿里云（即 `jdcloudcs` 换成 `aliyun`），再执行 `apt-get update` 更新，就可以解决问题。

手动尝试了下，果然可以了。

## 一键脚本

不过这个手动修改对于不擅长使用终端编辑文件的我还是有点麻烦的，干脆让 AI 来帮忙写个一键脚本，然后再重装一次系统试了下，完美解决～

```bash
sed -i '/^deb cdrom/s/^/#/; s/jdcloudcs/aliyun/g' /etc/apt/sources.list && apt-get update
```

> 脚本解释：
> 
> 这个脚本的作用是对 `/etc/apt/sources.list` 文件进行编辑和更新软件包信息。以下是脚本执行的步骤：
> 
> 1. 注释掉以 `deb cdrom` 开头的行：
>    使用 `sed -i '/^deb cdrom/s/^/#/' /etc/apt/sources.list`，将文件中以 `deb cdrom` 开头的行用 `#` 注释掉。这一操作使得这些行在包管理时被忽略。
> 2. 替换源地址中的 `jdcloudcs` 为 `aliyun`：
>    使用 `sed -i 's/jdcloudcs/aliyun/g' /etc/apt/sources.list`，将所有包含 `jdcloudcs` 的地方替换为 `aliyun`。这通常用于更改软件源地址。
> 3. 更新软件包索引：
>    使用 `apt-get update` 来更新软件包索引，以便系统知道软件源中的最新软件包信息。