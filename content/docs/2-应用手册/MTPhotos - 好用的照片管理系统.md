---
created: 2024-12-10
updated: 2024-12-10
share: true
date: 2024-12-10
lastmod: 2024-12-10
title: MTPhotos - 好用的照片管理系统
---

MT Photos 是一款闭源付费的自托管照片管理系统，和知名的开源照片管理系统 `Immich` 相比，部署更简单，更符合国人习惯。支持试用 1 个月，永久版价格 118 元（偶尔活动价 99 元）。

[官网](https://mtmt.tech/)｜[文档](https://mtmt.tech/docs/start/introduction)｜[购买](https://auth.mtmt.tech/buy)

我用到的主要功能如下：
- 使用 Docker 部署在群晖 Nas 中
- 移动端 App 支持手机照片自动备份
	- App 备份的照片自动按拍摄时间重命名
	- App 备份的照片自动按年月目录分类
- 支持添加外部图库（需要在部署时映射好存储卷）
- 支持 AI 识别人脸、场景、文本、GPS（内置 API 够用）
- 支持按时间线、人物、地点、场景、相册方式浏览照片
- 支持按以文搜图模式搜索照片，支持那年今日

其余多用户、分享、自定义 API、两步验证等功能自己暂时用不到。

## 我的实践

- 2024-12-01 尝试 Immich+AI 失败，开始试用 MT-Photos
- 2024-12-10 趁活动 99 元下单永久订阅
- 按照 [教程](https://mtmt.tech/docs/example/dsm2) 部署在家中群晖 Nas 上
- 使用 [App](https://mtmt.tech/docs/start/app) 在手机上设置好自动备份
- 历史照片使用外部图库方式暂时先一股脑映射进去

#### 计划

- 在群晖 Nas 中使用 Cloud Sync 同步到腾讯云 COS
- 外部图库的为历史多年多处备份，未去重、未整理
- 目前服务端仅在内网访问，外出时 App 无法查看照片