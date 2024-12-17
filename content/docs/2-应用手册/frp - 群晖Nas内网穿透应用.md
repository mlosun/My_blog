---
created: 2024-12-17
updated: 2024-12-17
share: true
date: 2024-12-17
lastmod: 2024-12-17
title: frp - 群晖Nas内网穿透应用
weight: 0
---

## 介绍

frp 是一个专注于内网穿透的高性能的反向代理应用，支持 TCP、UDP、HTTP、HTTPS 等多种协议，且支持 P2P 通信。可以将内网服务以安全、便捷的方式通过具有公网 IP 节点的中转暴露到公网。

[仓库](https://github.com/fatedier/frp) | [文档](https://gofrp.org/zh-cn/)

## 我的实践

> frp 分为服务端和客户端，一般使用 frps（server） 和 frpc（client） 表示。
> 以下适用于当前 0.61.0 版本

#### 准备工作

1. 云服务器使用 1Panel 面板
2. 群晖 Nas 添加矿神套件源 `https://spk7.imnks.com`

#### 部署 frps

1. 在云服务器的 1Panel 应用商店搜索 `frp 服务端` 并安装
2. 记录下**服务端口**（默认 7000）、**Dashboard 端口**（默认 7500）、**密钥**（即 token）
3. 服务器防火墙放行**服务端口**和 **Dashboard 端口**
4. 可通过访问**公网 ID+Dashboard 端口**的方式查看服务端仪表盘

#### 部署 frpc

1. 在群晖 Nas 的套件中心搜索 `Frpc客户端` 并安装
2. 打开应用（即 frpc 配置文件）
3. 配置全局参数

	```
	serverAddr = "0.0.0.0" # 云服务器的公网IP
	serverPort = 1234 # frps配置的服务端口
	auth.method = "token" # 默认token
	auth.token = "token" # frps配置的密钥
	```

4. 配置内网服务（每项服务都单独配置一套）

	```
	[[proxies]]
	name = "app" # 服务名称，不可重复
	type = "tcp" # 常规使用tcp即可
	localIP = "127.0.0.1" # 本机的服务就用127.0.0.1
	localPort = 1234 # 服务在本机的端口号
	remotePort = 1234 # 公网IP的端口，记得在云服务器上放行
	```