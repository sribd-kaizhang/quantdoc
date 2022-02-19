---
title: 市场指数
tags: [single_sourcing]
last_updated: February 16, 2022
keywords: data management
summary: "This page is for data interface."
sidebar: mydoc_sidebar
permalink: mydoc_get_index_data.html
folder: mydoc
---

## 指数行情

### 日线行情


接口：`get_index_daily`  
描述：返回一段时期内的指数日行情数据

__输入参数__：  

|名称 |类型 |必选 |描述 |  
| --- | --- | --- | --- |
|`index_code`|str|Y|指数代码，其中'000001'：上证综合指数；'000002'：上证综合A股指数；'000003'：上证综合B股指数；'399106'：深证综合指数；'399107'：深证综合A股指数；'399108'：深证综合B股指数；'399001'：深证成份指数；'000010'：上证180；'399004'：深证100；'000300'：沪深300；'000902'：中证流通；'000903'：中证100；'399903'：中证100；'399329'：中小板指；'000020':上证中型企业综合指数；|
|`from_date`|str|Y|起始日期，日期格式为`'yyyy-MM-dd'`|  
|`to_date`|str|Y|结束日期，日期格式为`'yyyy-MM-dd'`| 

__输出参数__:

|名称|类型|描述|  
|----|----|----|
|`index_code`|str|指数代码|
|`trade_date`|str|交易日期|
|`Daywk`|float|星期|
|`Opnindex`|float|每日交易中的第一条指数|
|`Hiindex`|float|每日交易中的最高一条指数|
|`Loindex`|float|每日交易中的最低一条指数|
|`Clsindex`|float|每日交易中的最后一条指数|
|`Retindex`|float|指数日回报率|

### 月线行情

接口：`get_index_monthly`  
描述：返回一段时期内的指数月行情数据

__输入参数__：  

|名称 |类型 |必选 |描述 |  
| --- | --- | --- | --- |
|`index_code`|str|Y|指数代码，其中'000001'：上证综合指数；'000002'：上证综合A股指数；'000003'：上证综合B股指数；'399106'：深证综合指数；'399107'：深证综合A股指数；'399108'：深证综合B股指数；'399001'：深证成份指数；'000010'：上证180；'399004'：深证100；'000300'：沪深300；'000902'：中证流通；'000903'：中证100；'399903'：中证100；'399329'：中小板指；'000020':上证中型企业综合指数；|
|`from_month`|str|Y|起始月份，日期格式为`'yyyy-MM'`|  
|`to_month`|str|Y|终止月份，日期格式为`'yyyy-MM'`| 

__输出参数__:

|名称|类型|描述|  
|----|----|----|
|`index_code`|str|指数代码|
|`trade_month`|str|交易月份|
|`Opnindex`|float|每月交易中的第一条指数|
|`Hiindex`|float|每月交易中的最高一条指数|
|`Loindex`|float|每月交易中的最低一条指数|
|`Clsindex`|float|每月交易中的最后一条指数|
|`Retindex`|float|指数月回报率|

## 市场行情

### 市场收益率

接口：`get_mkt_ret`  
描述：返回A股市场收益率数据

__输入参数__： 无  

__输出参数__:

|名称|类型|描述|  
|----|----|----|
|`trade_date`|str|交易日期|
|`mkt_ret`|float|A股所有股票（不包含科创版、创业板）按流通市值加权平均法计算的考虑现金红利再投资的日市场回报率|

### 无风险利率 

接口：`get_risk_free_rate`  
描述：返回无风险利率

__输入参数__：无

__输出参数__:

|名称|类型|描述|  
|----|----|----|
|`Nrr1`|str|无风险利率基准,'NRI01':定期-整存整取-一年利率|
|`trade_date`|str|交易日期|
|`Nrrdata`|float|年化无风险利率|
|`Nrrdaydt`|float|日度化无风险利率|
|`Nrrwkdt`|float|周度化无风险利率|
|`Nrrmtdt`|float|月度化无风险利率|
