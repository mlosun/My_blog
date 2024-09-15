---
created: 2024-09-14
updated: 2024-09-14
share: true
date: 2024-09-14
lastmod: 2024-09-14
tags:
  - Hugo
categories:
  - 技巧
title: Hugo 的常用命令
slug: Common-Hugo-Commands
---

> 本文基于的 hugo 版本：
> ```shell
> hugo v0.134.2+extended darwin/amd64 BuildDate=2024-09-10T10:46:33Z VendorInfo=brew
> ```
> - 版本号：0.134.2 扩展版
> - 操作系统：macOS 64 位
> - 构建时间：2024 年 9 月 10 日
> - 安装来源：Homebrew 包管理器

## 常用命令

- 查看 hugo 版本

	```shell
	hugo version
	```

- 创建一个新站点，存储在 `newblog` 文件夹内

	```shell
	hugo new site newblog
	```

- 创建一篇新文章，路径为 `content/posts/newpost.md`

	```shell
	hugo new posts/newpost.md
	```

- 本地预览（生成静态文件并启动 web 服务） http://localhost:1313/

	```shell
	hugo server -w -D
	```

## hugo help 翻译

安装好 hugo 后，在终端输入 `hugo help` 会输出如下内容：

```shell
hugo is the main command, used to build your Hugo site.

Hugo is a Fast and Flexible Static Site Generator
built with love by spf13 and friends in Go.

Complete documentation is available at https://gohugo.io/.

Usage:
  hugo [flags]
  hugo [command]

Available Commands:
  completion  Generate the autocompletion script for the specified shell
  config      Print the site configuration
  convert     Convert your content to different formats
  deploy      Deploy your site to a Cloud provider.
  env         Print Hugo version and environment info
  gen         A collection of several useful generators.
  help        Help about any command
  import      Import your site from others.
  list        Listing out various types of content
  mod         Various Hugo Modules helpers.
  new         Create new content for your site
  server      A high performance webserver
  version     Print Hugo version and environment info

Flags:
  -b, --baseURL string             hostname (and path) to the root, e.g. https://spf13.com/
  -D, --buildDrafts                include content marked as draft
  -E, --buildExpired               include expired content
  -F, --buildFuture                include content with publishdate in the future
      --cacheDir string            filesystem path to cache directory
      --cleanDestinationDir        remove files from destination not found in static directories
      --clock string               set the clock used by Hugo, e.g. --clock 2021-11-06T22:30:00.00+09:00
      --config string              config file (default is hugo.yaml|json|toml)
      --configDir string           config dir (default "config")
  -c, --contentDir string          filesystem path to content directory
      --debug                      debug output
  -d, --destination string         filesystem path to write files to
      --disableKinds strings       disable different kind of pages (home, RSS etc.)
      --enableGitInfo              add Git revision, date, author, and CODEOWNERS info to the pages
  -e, --environment string         build environment
      --forceSyncStatic            copy all files when static is changed.
      --gc                         enable to run some cleanup tasks (remove unused cache files) after the build
  -h, --help                       help for hugo
      --ignoreCache                ignores the cache directory
      --ignoreVendorPaths string   ignores any _vendor for module paths matching the given Glob pattern
  -l, --layoutDir string           filesystem path to layout directory
      --logLevel string            log level (debug|info|warn|error)
      --minify                     minify any supported output format (HTML, XML etc.)
      --noBuildLock                don't create .hugo_build.lock file
      --noChmod                    don't sync permission mode of files
      --noTimes                    don't sync modification time of files
      --panicOnWarning             panic on first WARNING log
      --poll string                set this to a poll interval, e.g --poll 700ms, to use a poll based approach to watch for file system changes
      --printI18nWarnings          print missing translations
      --printMemoryUsage           print memory usage to screen at intervals
      --printPathWarnings          print warnings on duplicate target paths etc.
      --printUnusedTemplates       print warnings on unused templates.
      --quiet                      build in quiet mode
      --renderSegments strings     named segments to render (configured in the segments config)
  -M, --renderToMemory             render to memory (mostly useful when running the server)
  -s, --source string              filesystem path to read files relative from
      --templateMetrics            display metrics about template executions
      --templateMetricsHints       calculate some improvement hints when combined with --templateMetrics
  -t, --theme strings              themes to use (located in /themes/THEMENAME/)
      --themesDir string           filesystem path to themes directory
      --trace file                 write trace to file (not useful in general)
  -v, --verbose                    verbose output
  -w, --watch                      watch filesystem for changes and recreate as needed

Use "hugo [command] --help" for more information about a command.
```

借助 AI 对其进行翻译

```shell
Hugo 是主命令，用于构建你的 Hugo 网站。

Hugo 是一个快速且灵活的静态网站生成器，
由 spf13 和朋友们用 Go 语言编写，满怀热情打造。

完整的文档可以在 https://gohugo.io/ 上找到。

用法:
  hugo [flags]
  hugo [command]

可用命令:
  completion  为指定的 shell 生成自动补全脚本
  config      输出站点配置
  convert     将你的内容转换为不同格式
  deploy      将你的站点部署到云服务提供商
  env         输出 Hugo 版本和环境信息
  gen         一些有用的生成器集合
  help        获取关于某个命令的帮助
  import      从其他平台导入你的站点
  list        列出各种类型的内容
  mod         各种 Hugo 模块助手
  new         为你的站点创建新内容
  server      一个高性能的 Web 服务器
  version     输出 Hugo 版本和环境信息

选项（Flags）:
  -b, --baseURL string             主机名 (及路径)，例如 https://spf13.com/
  -D, --buildDrafts                包含标记为草稿的内容
  -E, --buildExpired               包含过期内容
  -F, --buildFuture                包含发布日期在未来的内容
      --cacheDir string            文件系统缓存目录的路径
      --cleanDestinationDir        从目标目录中移除未在静态目录中找到的文件
      --clock string               设置 Hugo 使用的时钟，例如 --clock 2021-11-06T22:30:00.00+09:00
      --config string              配置文件 (默认是 hugo.yaml|json|toml)
      --configDir string           配置目录 (默认 "config")
  -c, --contentDir string          内容目录的文件系统路径
      --debug                      输出调试信息
  -d, --destination string         写入文件的文件系统路径
      --disableKinds strings       禁用不同类型的页面 (首页, RSS 等)
      --enableGitInfo              将 Git 版本、日期、作者和 CODEOWNERS 信息添加到页面中
  -e, --environment string         构建环境
      --forceSyncStatic            静态文件更改时复制所有文件
      --gc                         启用构建后的清理任务 (移除未使用的缓存文件)
  -h, --help                       获取 Hugo 的帮助信息
      --ignoreCache                忽略缓存目录
      --ignoreVendorPaths string   忽略与给定 Glob 模式匹配的模块路径中的任何 _vendor
  -l, --layoutDir string           布局目录的文件系统路径
      --logLevel string            日志级别 (debug|info|warn|error)
      --minify                     压缩任何支持的输出格式 (HTML, XML 等)
      --noBuildLock                不创建 .hugo_build.lock 文件
      --noChmod                    不同步文件的权限模式
      --noTimes                    不同步文件的修改时间
      --panicOnWarning             在首次出现 WARNING 日志时停止程序
      --poll string                设置轮询间隔，例如 --poll 700ms，使用轮询方式监控文件系统变化
      --printI18nWarnings          输出缺失的翻译警告
      --printMemoryUsage           定期输出内存使用信息
      --printPathWarnings          输出重复目标路径等警告
      --printUnusedTemplates       输出未使用的模板警告
      --quiet                      静默模式构建
      --renderSegments strings     渲染命名的部分 (在配置中定义)
  -M, --renderToMemory             渲染到内存 (主要用于运行服务器时)
  -s, --source string              读取文件的相对路径
      --templateMetrics            显示模板执行的指标
      --templateMetricsHints       结合 --templateMetrics 使用时计算一些优化提示
  -t, --theme strings              使用的主题 (位于 /themes/THEMENAME/)
      --themesDir string           主题目录的文件系统路径
      --trace file                 将跟踪信息写入文件 (通常不需要)
  -v, --verbose                    输出详细信息
  -w, --watch                      监视文件系统的变化并根据需要重新生成

使用 "hugo [command] --help" 获取某个命令的更多信息。
```