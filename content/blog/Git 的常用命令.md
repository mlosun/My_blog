---
share: true
date: 2024-09-15
lastmod: 2024-09-15
tags:
  - Git
categories:
  - 技巧
title: Git 的常用命令
slug: Common-Git-Commands
---
  
> 本文基于的 Git 版本：  
> ```shell  
> git version 2.46.0  
> ```  
> - 版本号：2.46.0  
> - 操作系统：macOS 64 位  
> - 构建时间：2024 年 7 月 29 日  
  
## 常用命令  
  
*由于我很少使用命令行进行 Git 操作，所以我常用的命令往往是查询或设置类的命令*  
- 查看 git 版本  
  
	```shell  
	git -v   
	```  
  
- 用户名和邮箱  
  
	```shell  
	# 设置全局的用户名和邮箱  
	git config --global user.name "username"  
	git config --global user.email "username@email.com"  
	  
	# 设置当前仓库的用户名和邮箱  
	git config user.name "username"  
	git config user.email "username@email.com"  
	  
	# 查看当前仓库的用户名和邮箱  
	git config user.name  
	git config user.email  
	```  
  
- 查看当前配置  
  
	```shell  
	git config --list  
	```  
  
- 查看当前分支和远程分支  
  
	```shell  
	git branch -a  
	```  
  
- 查看远程仓库信息  
  
	```shell  
	git remote -v  
	```  
  
- 查看当前状态（查看哪些文件被修改或暂存）  
  
	```shell  
	git status  
	```  
  
- 查看文件差异（比较工作目录和暂存区的差异）  
  
	```shell  
	git diff  
	```  
  
## Git help  
  
在终端输入 `git help`，输出以下内容  
  
```shell  
用法：git [-v | --version] [-h | --help] [-C <路径>] [-c <名称>=<取值>]  
           [--exec-path[=<路径>]] [--html-path] [--man-path] [--info-path]  
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] ["--no-lazy-fetch]  
           [--no-optional-locks] [--no-advice] [--bare] [--git-dir=<路径>]  
           [--work-tree=<路径>] [--namespace=<名称>]  
           [--config-env=<名称>=<环境变量>] <命令> [<参数>]  
  
这些是各种场合常见的 Git 命令：  
  
开始一个工作区（参见：git help tutorial）  
   clone     克隆仓库到一个新目录  
   init      创建一个空的 Git 仓库或重新初始化一个已存在的仓库  
  
在当前变更上工作（参见：git help everyday）  
   add       添加文件内容至索引  
   mv        移动或重命名一个文件、目录或符号链接  
   restore   恢复工作区文件  
   rm        从工作区和索引中删除文件  
  
检查历史和状态（参见：git help revisions）  
   bisect    通过二分查找定位引入 bug 的提交  
   diff      显示提交之间、提交和工作区之间等的差异  
   grep      输出和模式匹配的行  
   log       显示提交日志  
   show      显示各种类型的对象  
   status    显示工作区状态  
  
扩展、标记和调校您的历史记录  
   branch    列出、创建或删除分支  
   commit    记录变更到仓库  
   merge     合并两个或更多开发历史  
   rebase    在另一个分支上重新应用提交  
   reset     重置当前 HEAD 到指定状态  
   switch    切换分支  
   tag       创建、列出、删除或校验一个 GPG 签名的标签对象  
  
协同（参见：git help workflows）  
   fetch     从另外一个仓库下载对象和引用  
   pull      获取并整合另外的仓库或一个本地分支  
   push      更新远程引用和相关的对象  
  
命令 'git help -a' 和 'git help -g' 显示可用的子命令和一些概念帮助。  
查看 'git help <命令>' 或 'git help <概念>' 以获取给定子命令或概念的  
帮助。  
有关系统的概述，查看 'git help git'。  
```