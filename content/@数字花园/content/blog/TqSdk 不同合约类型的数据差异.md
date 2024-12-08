---
created: 2024-10-27
updated: 2024-12-08
share: true
title: TqSdk 不同合约类型的数据差异
date: 2024-09-17
lastmod: 2024-09-17
tags:
  - Tqsdk
categories:
  - Tqsdk
slug: tqsdk-ins_class-diff
---

## 合约类型

根据 [query_symbol_info](https://doc.shinnytech.com/tqsdk/latest/reference/tqsdk.api.html#tqsdk.TqApi.query_symbol_info) 得知，Tqsdk 里的合约类型可能的值有：

- `FUTURE` 期货
- `CONT` 主连
- `COMBINE` 组合
- `INDEX` 指数
- `OPTION` 期权
- `STOCK` 股票

这里常用的就是 `FUTURE` 和 `CONT`。

通常使用 `FUTURE` 就可以了，但是在做一些长周期的回测时，需要考虑到主力合约变更的情况。[官方文档对这个问题的描述](https://doc.shinnytech.com/tqsdk/latest/usage/backtest.html#backtest-underlying-symbol) 是使用主连合约，然后使用 `quote.underlying_symbol` 获取回测当时的标的合约。

在实际应用时，发现 `FUTURE` 和 `CONT` 不同合约类型，在订阅 `kline`、`quote`、`tick` 等数据时还是有一些细微区别的，在这里整理并做记录。

## 测试代码

以下是测试时使用的代码，测试时 `CZCE.AP501` 是当前主力，且持空仓 13 手。

```python
from tqsdk import TqApi,TqAuth,TqKq
api = TqApi(account = TqKq(),auth=TqAuth("信易账户","信易密码"))

FUTURE = 'CZCE.AP501'
CONT = 'KQ.m@CZCE.AP'

print('========== quote ==========')
print(api.get_quote(FUTURE))
print(api.get_quote(CONT))

print('========== kline ==========')
print(api.get_kline_serial(FUTURE,86400).iloc[0])
print(api.get_kline_serial(CONT,86400).iloc[0])

print('========== tick ==========')
print(api.get_tick_serial(FUTURE).iloc[0])
print(api.get_tick_serial(CONT).iloc[0])

print('========== position ==========')
print(api.get_position(FUTURE))
print(api.get_position(CONT))

print('========== symbol_info ==========')
print(api.query_symbol_info(FUTURE).iloc[0])
print(api.query_symbol_info(CONT).iloc[0])

api.close()
```

## 数据差异

> 图片中左侧是 `FUTURE`，右侧是 `CONT`

### get_quote 差异

[接口文档](https://doc.shinnytech.com/tqsdk/latest/reference/tqsdk.api.html#tqsdk.TqApi.get_quote)
![get_quote.png](https://img.mlosun.com/images/2024/202409180013108.png)

### get_kline_serial 差异

[接口文档](https://doc.shinnytech.com/tqsdk/latest/reference/tqsdk.api.html#tqsdk.TqApi.get_kline_serial)
![get_kline_serial.png](https://img.mlosun.com/images/2024/202409180014884.png)

### get_tick_serial 差异

[接口文档](https://doc.shinnytech.com/tqsdk/latest/reference/tqsdk.api.html#tqsdk.TqApi.get_tick_serial)
![get_tick_serial.png](https://img.mlosun.com/images/2024/202409180016177.png)

### get_position 差异

[接口文档](https://doc.shinnytech.com/tqsdk/latest/reference/tqsdk.api.html#tqsdk.TqApi.get_position)
![get_position.png](https://img.mlosun.com/images/2024/202409180016765.png)

### query_symbol_info 差异

[接口文档](https://doc.shinnytech.com/tqsdk/latest/reference/tqsdk.api.html#tqsdk.TqApi.query_symbol_info)
![query_symbol_info.png](https://img.mlosun.com/images/2024/202409180016429.png)
