---
share: true
date: 2024-10-06
lastmod: 2024-10-06
tags:
  - python
  - pipreqs
categories:
  - Python
title: Python库：pipreqs 生成项目依赖文件
slug: python-pipreqs
---

> `pipreqs` 是一个 Python 库，它的主要功能是根据项目代码中的 `import` 语句自动生成 `requirements.txt` 文件。这个文件列出了项目所依赖的第三方库和版本，便于环境的重现和部署。

## 安装

你可以通过以下命令来安装 `pipreqs`：

```bash
pip install pipreqs
```

## 用法

安装好后就可以在项目根目录下通过如下命令生成 `requirements.txt` 文件。

```bash
pipreqs . --encoding=utf-8 --force
```

## 选项

- `<path>`: 指定要扫描的目录路径，如果未提供，则默认使用当前目录。
- `--use-local`: 仅从本地安装的库中获取版本信息，而不通过 PyPI 远程查找。
- `--pypi-server <url>`: 使用自定义的 PyPI 源地址来获取包的信息。
- `--proxy <url>`: 使用代理服务器进行网络请求。代理地址可以直接在命令行指定，或者通过环境变量设置。
- `--debug`: 启用调试模式，输出详细的调试信息。
- `--ignore <dirs>`: 忽略特定的目录，避免在这些目录中查找依赖。多个目录可以用逗号分隔。
- `--no-follow-links`: 如果项目中有符号链接文件夹，`pipreqs` 默认会跟随这些链接。使用此参数可以禁止这一行为。
- `--encoding <charset>`: 为打开文件指定编码类型（默认是 `utf-8`）。
- `--savepath <file>`: 自定义生成的 `requirements.txt` 文件保存路径。
- `--print`: 将依赖项直接输出到终端，而不生成 `requirements.txt` 文件。
- `--force`: 如果 `requirements.txt` 文件已经存在，使用此参数强制覆盖。
- `--diff <file>`: 比较指定的 `requirements.txt` 文件中的依赖与项目实际导入的依赖，查看差异。
- `--clean <file>`: 清理指定的 `requirements.txt` 文件，移除那些在项目中未实际导入的库。
- `--mode <scheme>`: 指定生成 `requirements.txt` 文件中依赖的版本控制方式，支持以下三种：
	  - `compat`: 使用兼容版本，如 `Flask~=1.1.2`，表示兼容 `1.1.x` 版本。
	  - `gt`: 使用大于等于版本号的模式，如 `Flask>=1.1.2`。
	  - `no-pin`: 不指定版本号，如 `Flask`。
- `--scan-notebooks`: 在项目的 Jupyter Notebook 文件中查找 `import` 语句，适合那些使用 `.ipynb` 文件的项目。 

## 延伸

1. 生成 `requirements.txt` 文件也可以直接使用 pip 的自带命令 `pip freeze > requirements.txt`，只是这样会将本地环境中的所有三方包都丢进去，通常情况下这并不是我们想要的。
2. 可以使用如下命令一次性安装 `requirements.txt` 里的全部包

	```bash
	pip install -r requirements.txt
	```
