---
created: 2024-10-27
updated: 2024-10-27
share: true
date: 2024-10-27
lastmod: 2024-10-27
tags:
  - 技术
categories:
  - MacOS
  - 终端
  - 技巧
title: Mac 终端技巧合集
slug: macos-terminal-tips
---

## 启动时切换到指定目录

> 对于 zsh 用户

1. 打开终端。
2. 输入以下命令来编辑你的 `.zshrc` 文件（如果不存在，这个命令会创建一个）：

    ```shell
    nano ~/.zshrc
    ```

3. 在打开的文件中，添加以下行来设置你的工作目录：

    ```shell
    cd /path/to/your/directory #替换成你想要切换到的目录路径。
    ```

4. 保存并关闭文件（在 nano 编辑器中，使用 `Ctrl + X`，然后按 `Y`，最后按 `Enter`）。
5. 为了让更改生效，你需要重新加载 `.zshrc`，可以输入以下命令：

    ```shell
    source ~/.zshrc
    ```

这样，每次你打开终端时，它就会自动切换到你指定的目录。如果你使用的是其他 shell，步骤类似，只需找到对应的配置文件进行修改即可。

## 终端显示完整路径

> 对于 zsh 用户

1. 打开终端。
2. 输入以下命令来编辑你的 `.zshrc` 文件：

    ```shell
    nano ~/.zshrc
    ```

3. 在文件中添加或修改 `PROMPT` 变量，如下所示：

    ```shell
    PROMPT='%~ %# '
    ```

    这里 `%~` 代表当前目录的完整路径，`%#` 是提示符。如果你想要显示当前目录的最后一个部分，可以使用：

    ```shell
    PROMPT='%1~ %# '
    ```

4. 保存并关闭文件。
5. 重新加载 `.zshrc`：

    ```shell
    source ~/.zshrc
    ```