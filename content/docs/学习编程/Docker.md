---
created: 2024-12-01
updated: 2024-12-09
share: true
title: Docker
---

## 常用命令

> 仅列出目前自己常用的，更多命令可参考 [Docker 命令大全 | 菜鸟教程](https://www.runoob.com/docker/docker-command-manual.html)

- `docker ps` 列出 docker 容器，客获取**获取容器的 ID 和名称**
- `docker stats` 实时显示 docker 容器的**资源使用情况**
- `docker logs -f --tail 100 <容器ID或名称>` 实时显示的 100 条**容器日志**
- `docker compose up -d` 在当前目录下以后台模式运行 `docker-compose.yml` 内定义的容器

## 核心概念

- 镜像（Image）：镜像是 Docker 中的一个模板。
- 容器（Container）：容器是镜像运行时的实例。
- 仓库（Repository）：仓库用来存储镜像。

## 配置文件

- `Dockerfile` 定义如何构建一个镜像 [Docker Dockerfile \| 菜鸟教程](https://www.runoob.com/docker/docker-dockerfile.html)
- `docker-compose.yml` 定义和管理一个或多个容器 [Docker Compose \| 菜鸟教程](https://www.runoob.com/docker/docker-compose.html)