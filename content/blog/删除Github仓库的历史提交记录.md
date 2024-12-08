---
created: 2024-09-11
updated: 2024-12-08
share: true
date: 2024-09-12
lastmod: 2024-09-12
title: 删除Github仓库的历史提交记录
tags:
  - Gihub
  - Git
categories:
  - 技巧
slug: Delete-GitHub-commit
---

> 最近一段时间为了将在不同设备跑的程序日志汇总在一起分析，向 Github 的仓库上传了大量的 log 文件，导致仓库过大在拉取时频繁出错，但其余普通大小的仓库拉取就没问题。所以想着用删除历史提交的方式将仓库变小。

**注意：此操作有风险，需提前做好备份再执行。**

## 方法一：创建一个新的主分支

```shell
git checkout --orphan latest_branch # 将当前最新代码切换到新分支
git add -A # 暂存当前所有文件
git commit -m "init commit" # 提交暂存的文件
git branch -D main # 删除原有main分支
git branch -m main # 将当前分支重命名为main
git push -f origin main # 推送到远端的main分支
```

## 方法二：重新初始化 git

```shell
# 首先手动删除本地的.git目录
git init # 初始化新的git仓库
git add -A # 暂存当前所有文件
git commit -m "init commit" # 提交暂存的文件
git push -f https://github.com/username/repo.git  main # 使用 -f 强制推送到远端main分支
```