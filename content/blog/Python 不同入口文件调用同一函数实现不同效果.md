---
created: 2024-10-18
updated: 2024-10-18
share: true
date: 2024-10-18
lastmod: 2024-10-18
tags:
  - Python
  - 入口文件
categories:
  - Python
title: Python 不同入口文件调用同一函数实现不同效果
slug: python-func-diff-entry-and-effects
---

## 需求场景

在写量化交易程序的过程中，往往需要多次回测以验证策略及程序的可靠性。由于一些特别的原因，实盘时我需要从数据库去获取相应的参数，而回测时如果也从数据库拿参数，那就会很繁琐，所以我希望能在本地调试参数。

所以就期望有一种方法，就期望有一种方法，能够在不改变任何代码（包括参数）的情况下分别执行不同参数的回测、实盘代码。

于是想到了使用不同的文件入口，比如 `strategy.py` 是实盘模式的运行入口，`backtest.py` 是回测模式的运行入口。

但是这样就产生一个问题，当我业务逻辑调整（目前在调试阶段还是比较频繁的）时，两个文件都需要同时去改，这样又是就需要花大量的时间去“找不同”。

但如果这两个入口文件，在调用同一个函数却能实现不同效果，那就完美了。

## 解决方案

在对比了 AI 给到的 N 种方案后（有一些方案限于我 python 水平一般，还无法理解），最终我选取了好理解、好操作的方案，在这里记录一下。

我有三个文件，分别是 `strategy.py`、`backtest.py` 、`config.py`，其中 `config.py` 是参数模块，负责输出参数，剩下两个是负责实盘和回测的入口文件

两个入口文件 `strategy.py` 和 `backtest.py` 的代码如下（两个文件代码完全相同）：

```python
import os
from config import 获取参数
入口文件名 = os.path.basename(__file__)
参数 = 获取参数(入口文件名)
print(参数)
```

参数模块 `config.py` 的代码如下

```python
def 获取参数(入口文件名):
    if 入口文件名 == "strategy.py":
        # 实际代码略
        参数 = 1
    elif 入口文件名 == "backtest.py":
        # 实际代码略
        参数 = 2
    return 参数
```

这样就能实现
- 运行 `strategy.py` 时，参数 = 1
- 运行 `backtest.py` 时，参数 = 2