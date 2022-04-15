---
title: 异象因子接口
tags: [single_sourcing]
last_updated: February 11, 2022
keywords: factor description
summary: "This page provides the functions to compute the anomaly factors."
sidebar: mydoc_sidebar
permalink: mydoc_factor_get_function.html
folder: mydoc
---

__因子库`factor_library`提供包括交易摩擦因子（市值因子、波动率因子、高阶距因子、流动性因子、Beta因子）、动量因子、价值因子、成长因子、盈利因子与财务流动性因子等六大类因子对应公司特征数据。其中，因子库包含`cmpt_factor`与`get_factor`两个模块，分别负责因子计算与因子提取。本部分将介绍因子数据提取模块`get_factor`。__

调用因子库前，需要导入`get_factor`模块：

```python
from quantools.factor_library import get_factor as gf
```



## 市值因子

接口：`get_factor`  
描述：根据指定日期，返回指定股票池的公司特征。当输入单个日期时（_trade_date_），函数返回输入日期前最后一个交易日盘后数据；当输入日期区间（_from_date_与_to_date_），函数返回输入日期区间内每月最后一个交易日盘后数据；

__输入参数__：  

|名称 |类型 |必选 |描述 |
| --- | --- | --- | --- |
|`factor_type`|str|N|因子类别，默认`'size'`，即市值因子；可选`'vol'`，即波动率因子; 可选`'mom'`，即动量因子; 可选`'liq'`，即流动性因子; 可选`'beta'`，即Beta因子; 可选`'value'`，即价值因子; 可选`'growth'`，即成长因子; 可选`'profit'`，即盈利因子；可选`'fina_liq'`，即财务流动性因子;|
| `from_date`   | str  | N    | 起始日期，日期格式为`'yyyy-MM-dd'`                           |
| `to_date`     | str  | N    | 终止日期，日期格式为`'yyyy-MM-dd'`                           |
| `trade_date`  | str  | N    | 交易日期，日期格式为`'yyyy-MM-dd'`                           |
| `pool`        | str  | N    |股票池，默认`'all_a_market'`即返回A股所有股票的因子值；可选`liquid_perc70`，即自定义的流动性股票池；|

__输出参数__:

_以市值因子为例：_

|名称 |类型 |描述 |
| --- |--- |--- |
|`trade_date`|str|交易日期|
|`stock_code`|str|股票代码|
|`mc`|float|总市值|
|`mc_log`|float|总市值对数|
|`circ_mc`|float|流动市值|
|`circ_mc_log`|float|流动市值对数|
|`mc_nonlinear`|float|非线性市值|
|`circ_to_total_mc_ratio`|float|流通市值占总市值比重&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|
