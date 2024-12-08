---
created: 2024-09-15
updated: 2024-09-15
share: true
date: 2024-09-15
lastmod: 2024-09-15
tags:
  - PicGo
  - Github
  - 图床
categories:
  - 折腾
title: 使用 PicGo 和 Github 搭建图床
slug: PicGo-Github
---

## Github 设置

- [创建](https://github.com/new) 一个新的 Github 仓库
	- 手动创建 `CNAME` 绑定域名（记得解析）
	- `Settings - Pages` 中
		- Branch 设置为 `main`
		- 勾选 Enforce HTTPS
- [创建](https://github.com/settings/tokens) 一个新的 Github Token

## PicGo 设置

- [下载](https://github.com/Molunerfinn/PicGo/releases/tag/v2.3.1) 并安装 PicGo v2.3.1
	- 截止目前（2024-09-15）
	- 最新的正式版是 v2.3.1
	- 最新的测试版是 v2.4.0-beta.8
	- 图床服务对功能无更多需求，稳定优先，所以使用最新的正式版即可
- 添加一个 Github 图床
	- 仓库名、分支名、Token 自行填写
	- 设定存储路径：我使用 `images/2024/`
	- 设定自定义域名：填写仓库里使用 `CNAME` 文件绑定的域名
- PicGo 设置
	- 开启自启：开
	- 时间戳重命名：开
	- 上传后自动复制 URL：开
	- 其余根据自身喜好设置即可
- 这样设置后，图片路径将是这样的格式 `https://域名/images/2024/202409152129743.jpg`

## 定期维护

这个图床我主要在 Hugo 和 Obsidian 中使用，这里有两个考虑点：
1. 自己在 Obsidian 笔记的过程中会产生一些冗余图片，很久后笔记失效同时对应的图片也会失效
2. 目前使用 Github 作为图床存储，但未来或许会迁移到腾讯云 COS 中，冗余图片会带来不必要的成本
所以我需要有一个定期维护的方案。

这个定期维护的周期，按月太频繁，所以考虑按年维护即可。如前面描述，存储路径被我设置为 `images/2024/`，到明年的话就会改成 `images/2025/`
这样的话每年清理一遍冗余图片即可。

（这样的方案也比较灵活，结合时间戳重命名，如果在 2025 年年初未能及时重新设置，那么图片路径会变成 `images/2024/2025***********.jpg`，也能够很方便的找出来）

## 应用设置

### Obsidian

使用插件 [Image auto upload](https://github.com/renmu123/obsidian-image-auto-upload-plugin)

安装后只需要确保 PicGo server 上传接口地址和端口与 PicGo 设置的一致即可（通常都是默认）

其余的一些个性化设置：
- 剪切板自动上传：开
- 图片描述：移除 image.png
- 图片大小后缀：空
- 应用网络图片：开
- 上传文件后移除源文件：开

### Hugo

由于我大部分 Hugo 的文章都是通过 Obsidian 完成，所以并不需要做什么特殊的设置。

只有少量单独的图片需要使用到图床时，手动上传到 `blog` 目录下即可。