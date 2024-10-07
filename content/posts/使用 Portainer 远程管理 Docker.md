---
share: true
date: 2024-10-07
lastmod: 2024-10-07
tags:
  - Docker
categories:
  - 技术
title: 使用 Portainer 远程管理 Docker
slug: portainer-manage-docker
---

本文内容基于 [6053537/portainer-ce - Docker Image | Docker Hub](https://hub.docker.com/r/6053537/portainer-ce) 的汉化版。

## 远程主机设置

1. 首先要已经安装 Docker，这个自然不必说。

2. 进入主机终端，输入命令：

	```bash
	nano /usr/lib/systemd/system/docker.service
	```

3. 然后做以下修改：

	```bash
	# 将这一行
	ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
	
	# 改为这样
	ExecStart=/usr/bin/dockerd -H tcp://0.0.0.0:2375 -H fd:// --containerd=/run/containerd/containerd.sock
	```

4. 最后再重启 Docker 即可

	```bash
	systemctl daemon-reload
	systemctl restart docker
	```

5. 记得在服务器的防火墙放开 2375 端口

## Portainer 设置

1. 环境 - 添加环境 - 独立的 Docker
2. 选择 API 连接模式
3. Docker API URL 处填写被远程连接的主机 IP+ 端口，如 `6.6.6.6:2375`
4. 点击链接，完成。

## 参考

[部署 Portainer 来管理本地或远程的 Docker - Moeyukina's Blog](https://blog.moeyukina.top/index.php/2022/11/02/deploying-portainer-managing-docker/)