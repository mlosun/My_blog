---
created: 2024-09-10
updated: 2024-12-08
share: true
date: 2024-09-10
lastmod: 2024-10-27
title: Obsidian + Github + Hugo 一站式笔记发布工作流
tags:
  - Hugo
  - Obsidian
  - Github
  - 发布
categories:
  - 折腾
slug: Obsidian-Github-Hugo
---

> 这是我自己正在使用的工作流，里面参杂了一些不一定通用，但适合自己的配置项，请注意甄别。
> 
> 除非我不采取本方案发布笔记了，否则本文将长期更新。

## 在 Github 上部署 Hugo

### 创建仓库

在 Github 上 [创建](https://github.com/new) 一个仓库，命名为 `blog`（可以根据自己喜好命名），记得创建是选择 `Public` 并且勾选 `Add a README file`，其余默认即可。

创建完成后在 `Code` 按钮下进入 `Codespaces` 标签页，点击 `Create codespace on main` 创建一个线上开发环境，也就是一个线上版的 VScode。

### 初始化 Hugo 文件

然后就可以在这里直接初始化 hugo。当然，有代码洁癖的我决定直接手工进行初始化，接下来的操作均在 `Codespaces` 的终端中进行。

1. 安装主题
	这里我使用优雅的 MemE 主题（2024/10/27 注：已不再使用 MemE 主题，但此处仍以 MemE 主题为例）

	```shell
	git submodule add --depth 1 https://github.com/reuixiy/hugo-theme-meme.git themes/meme
	```

2. 创建配置文件
	这里是将主题的默认配置文件复制过来，执行完可以看到目录树已经出现了 `config.toml` 文件了

	```shell
	cp themes/meme/config-examples/zh-cn/config.toml config.toml
	```

3. 新建一篇文章
	创建文件 `content/posts/hello_world.md`

	```shell
	mkdir -p content/posts && echo -e "---\ntitle: hello world\ndate: 2024-09-10\n---\nhello world" > content/posts/hello_world.md
	```

4. 新建关于页面
	创建文件 `content/about/_index.md`

	```shell
	mkdir -p content/about && echo -e "---\ntitle: about\ndate: 2024-09-10\n---\nabout" > content/about/_index.md
	```

5. 绑定域名
	将 `YouDomain.com` 和 `www.YouDomain.com` 改为自己的域名。这里是利用了 Hugo 的 `static` 目录 [特性](https://gohugo.io/getting-started/directory-structure/#static) ，绑定完成后不要忘记解析域名。

	```shell
	mkdir -p static && echo -e "YouDomain.com\nwww.YouDomain.com" > static/CNAME
	```

6. 保存并提交代码
	使用 git 提交代码并推送到远端。或者像在 VScode 里，在右侧边栏的源代码管理处用 git 提交你的代码

	```shell
	git add . && git commit -m "init hugo" && git push origin main
	```

	这时候目录树的结构应该和下面是一样的

	```
	blog/
	├── content/
	│   ├── posts/
	│   │   └── hello_world.md
	│   └── about/
	│       └── _index.md
	├── static/
	│   └── CNAME
	├── themes/
	│   └── meme/   [省略文件内容]
	├── .gitmodules
	├── config.toml
	└── README.md
	```

### 配置 Github Actions

Hugo 的文件部署提交完毕后，还需要利用 Github Actions 进行自动化部署。
1. 在 [这里](https://github.com/settings/tokens) 生成一个 Github Token（classic，repo 权限，无有效期）
2. 在仓库的 `Settings` → `Secrets and variables` → `Actions` 中添加一个 `Secret`
	- Name 填入 `ACTION_ACCESS_TOKEN`
	- Secret 填入刚才生成的 Token
3. 在仓库根目录下创建文件 `.github/workflows/Deploy.yml`，内容如下

	```yml
	name: Build and Deploy
	
	on:
	  push:
	    branches:
	      - main
	    # 当推送到 main 分支时触发
	
	jobs:
	  build-deploy:
	    runs-on: ubuntu-latest
	    # 运行在最新版本的 Ubuntu 上
	
	    steps:
	      - name: Checkout
	        uses: actions/checkout@v4
	        with:
	          submodules: true # 确保检出子模块
	          fetch-depth: 0    # 获取完整历史记录
	        # 检出仓库代码并包含子模块
	
	      - name: Setup Hugo
	        uses: peaceiris/actions-hugo@v3
	        with:
	          hugo-version: "latest"
	          extended: true
	        # 设置 Hugo，安装最新版本的 Hugo 扩展版
	
	      - name: Update submodules
	        run: git submodule update --init --recursive
	        # 初始化并更新子模块
	
	      - name: Build
	        run: hugo
	        # 运行 Hugo 命令构建静态网站
	
	      - name: Deploy to GitHub Pages
	        uses: peaceiris/actions-gh-pages@v4
	        with:
	          github_token: ${{ secrets.ACTION_ACCESS_TOKEN }}
	          publish_branch: gh-pages
	          publish_dir: ./public
	        # 部署到 gh-pages 分支
	        # 使用由 GitHub 自动生成的 ACTION_ACCESS_TOKEN 进行身份验证
	        # 将构建后的 ./public 目录中的文件发布到 gh-pages 分支
	```

4. 提交后过一会，就会发现仓库多了一个 `gh-pages` 分支，里面是在本地部署后，`pubilc` 目录里的文件。
5. 在仓库的 `Settings` → `Pages` → `Build and deployment` 里选择
    -  Source 选择 `Deploy from a branch`
    -  Branch 选择 `gh-pages`
    - 记得勾选下面的 `Enforce HTTPS`

如无意外，等待域名解析完成后，就可以通过域名访问这个 Hugo 站点了。

后续就是修改配置文件 `config.toml` 和生产内容的事情了。

### 加餐：自动化部署到服务器

众所周知，访问 Github 会比较慢，所以有时也想将 Hugo 的源码保存在 Github，而生成的静态文件部署到国内的服务器上，那么可以采取下面的方式。

1. ssh 登录到服务器，输入命令 `ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`（改成自己的邮箱）
2. 一路默认回车后，就可以在 `~/.ssh` 目录下看到 `id_rsa`（私钥）和 `id_rsa.pub`（公钥）
3. 首先将公钥里的内容，复制到 `~/.ssh/authorized_keys` 文件中
4. 然后回到 Github 仓库，陆续添加如下 `Secret`
    1. `SERVER_PATH`，服务器上存储静态资源的路径
    2. `SERVER_HOST`，服务器 IP 地址
    3. `SERVER_PORT`，服务器 ssh 端口，一般为 22
    4. `SERVER_USER`，服务器 ssh 用户
    5. `SERVER_KEY`，前面生成的私钥内容填入这里
5. 在 `.github/workflows/Deploy.yml` 后面补充：

	```yml
	      - name: Deploy to Server
	        uses: burnett01/rsync-deployments@7.0.1
	        with:
	          switches: -avzr --delete
	          path: ./public
	          remote_path: ${{ secrets.SERVER_PATH }}
	          remote_host: ${{ secrets.SERVER_HOST }}
	          remote_port: ${{ secrets.SERVER_PORT }}
	          remote_user: ${{ secrets.SERVER_USER }}
	          remote_key: ${{ secrets.SERVER_KEY }}
	        # 通过 ssh 连接服务器，用 rsync 同步文件
	        # 服务器信息通过 GitHub Secrets 设置
	```

其实部署到 Github 仓库和服务器，主要是最后一步的 Deploy 不同，我看了很多人写的不同的 Actions 命令，基本上部署到 Github Pages 都是用的 `peaceiris/actions-gh-pages`，而部署到服务器的确是有很多种方法，在这里我也被 ssh key 这个坑阻挠了好久，最终找到了 `burnett01/rsync-deployments` 才搞定。

## 使用 Obsidian 发布 Hugo 内容

### 工作流原理

- 利用 Obsidian 的 [Enveloppe](https://github.com/Enveloppe/obsidian-enveloppe) 插件，可以将 Obsidian 仓库中 YMAL 区域有 `share: true` 标记的笔记，上传到 Github 的指定目录下。我这里将上传到 `content/posts` 目录下
- 利用 Obsidian 的 [Templater](https://github.com/SilentVoid13/Templater) 插件，根据 Enveloppe、Hugo、MemE 主题等特性，创建设定好 YAML 区域的模板，后续直接

### Enveloppe 设置

- Github config
	- API Type：APY 类型
	- Github username：用户名
	- Repository name：仓库名
	- GitHub token：可以与前面部署 Hugo 自动化的 Token 共用，也可以生成新的
	- Main branch：md 源码上传到哪个分支，我是 `main`
	- Automatically merge pull requests：是否自动合并，我是 `true`
- File paths
	- File tree in repository：仓库中的文件树 `Fixed Folder`
	- Root folder：默认目录，我是 `content/posts`

上面这些是保障插件可以正常运转的一些设置，其余的内容根据自身喜好即可。

### Templater 模板

创建一个 Templater 模板，内容是常用的文章 `Front matter`，用于快速插入。详细的选项可以在 [Hugo 文档](https://gohugo.io/content-management/front-matter/) 或者 [主题的文档](https://github.com/reuixiy/hugo-theme-meme?tab=readme-ov-file#supported-front-matter) 处查看。

```yml
share: # Enveloppe 插件允许上传的开关 一般为true
date:  # 发布日期 格式参考：2024-09-12
lastmod: # 修改日期 格式参考：2024-09-12
tags: # 标签 格式参考：["Hugo", "Obsidian", "Github", "发布"]
categories: # 分类 格式参考：["折腾"]
title: # 文章标题
slug: # 路径标识
```

### 发布流程

在 Obsidian 中创建笔记，插入刚创建的模板。然后如往常一样使用 obsidian 完善笔记内容即可。

完成文章内容后，在 Obsidian 文件列表中，右键 Upload 上传到 Github

稍等 Github Actions 运行完毕，即可访问～
