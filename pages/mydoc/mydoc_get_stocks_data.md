---
title: 股票数据
tags: [single_sourcing]
last_updated: February 16, 2022
keywords: data management
summary: "This page is for data interface."
sidebar: mydoc_sidebar
permalink: mydoc_get_stocks_data.html
folder: mydoc
---

## 基础数据

### 交易日历


接口：`get_trade_cal`  
描述：根据交易频率，返回指定一段时期内的交易日。  

__输入参数__：  

|名称|类型|描述|  
| --- | --- | --- | --- |  
|`from_date`|str|起始日期，日期格式为`'yyyy-MM-dd'`|  
|`end_date`|str|结束日期，日期格式为`'yyyy-MM-dd'`| 
|`freq`|str|频率，默认'daily';若选择'monthly'，返回一段时期内每月最后一个交易日日期|    

__输出参数__:

|名称|类型|描述|
|----|----|----|
|`trade_date`|str|交易日日期|  

### 行业分类

接口：`get_industry`  
描述：获取股票行业分类
__输入参数__：  

|名称|类型|描述|  
| --- | --- | --- |  
|`industry_typ`|str|分类标准，默认'zhengjian'，即2012版证监会行业分类；可选‘shenwan’，即2021版申万行业分类|

__输出参数__:

|名称|类型|描述|
|----|----|----|
|`stock_code`|str|股票代码|
|`industry`|str|行业分类|  

### 风险警示股

接口：`get_st_stocks`  
描述：获取指定日期的ST股票代码  
__输入参数__：  

|名称|类型|描述|  
| --- | --- | --- |  
|trade_date|str|交易日期，日期格式为`'yyyy-MM-dd'`|  

__输出参数__:

列表，元素为指定日期的ST股票代码。  

### 新上市股票

接口：`get_new_stocks_code`  
描述：返回新上市股票代码  
__输入参数__：  

|名称|类型|描述|
| --- | --- | --- |
|trade_date|str|交易日期，日期格式为`'yyyy-MM-dd'`|
|days|int|上市最短天数，上市不足_days_天的股票将被认定为次新股|

__输出参数__:

列表，元素为指定日期的次新股股票代码。

### 股票池

接口：`get_stocks_pool`  
描述：返回股票池
__输入参数__： 

|名称|类型|描述|  
| --- | --- | --- |  
|trade_date|str|交易日期，日期格式为`'yyyy-MM-dd'`|  
|from_date|str|起始日期，日期格式为`'yyyy-MM-dd'`|  
|end_date|str|终止日期，日期格式为`'yyyy-MM-dd'`|  
|pool|str|股票池，默认为'hushen300'，可为'zhongzheng500','liquid_perc70'|  

__输出参数__:

|名称|类型|描述|  
|----|---|---| 
|stocks_pool|dataframe|交易日股票池数据|  


## 行情数据

### 日线行情

接口：`get_stocks_daily`  
描述：返回股票日频行情数据
__输入参数__： 

|名称|类型|描述|  
| --- | --- | --- |  
|stock_code|list/str|股票代码，形如'000001'，以指定特定股票数据或股票代码列表；可选项，默认为全部股票|  
|trade_date|str|交易日期，日期格式为`'yyyy-MM-dd'`；trade_date和(from_date,end_date)二选其一，可分别获取单日/周期内股票日线行情数据|  
|from_date|str|起始日期，日期格式为`'yyyy-MM-dd'`|  
|end_date|str|终止日期，日期格式为`'yyyy-MM-dd'`|  
|pool|str|股票池，包括'all_a_market','hushen300','zhongzheng500','liquid_perc70'，默认为全部A股|  

__输出参数__:

|名称|类型|描述|  
|----|---|---| 
|output|dataframe|指定股票代码的日行情数据|  


### 月线行情

接口：`get_stocks_monthly`  
描述：返回股票月频行情数据
__输入参数__： 

|名称|类型|描述|  
| --- | --- | --- |  
|stock_code|list/str|股票代码，例如'000001'，以指定特定股票数据或股票代码列表；可选项，默认为全部股票|  
|trade_date|str|交易日期，日期格式为`'yyyy-MM-dd'`；trade_date和(from_date,end_date)二选其一，可分别获取单日/周期内股票月线行情数据|  
|from_date|str|起始日期，日期格式为`'yyyy-MM-dd'`|  
|end_date|str|终止日期，日期格式为`'yyyy-MM-dd'`|  

__输出参数__:

|名称|类型|描述|  
|----|---|---|  
|output|dataframe|指定股票代码的月行情数据|  


### 每日指标

接口：`get_daily_basic`  
描述：返回股票日频指标数据  
__输入参数__： 

|名称|类型|描述|  
| --- | --- | --- |  
|trade_date|str|交易日期，日期格式为`'yyyy-MM-dd'`|  
|from_date|str|起始日期，日期格式为`'yyyy-MM-dd'`|  
|end_date|str|终止日期，日期格式为`'yyyy-MM-dd'`|  

__输出参数__:

|名称|类型|描述|  
|----|---|---|  
|output|dataframe|交易日指标数据|  

### 停复牌信息

接口：`get_daily_suspended`  
描述：返回股票日频停复牌数据  
__输入参数__： 

|名称|类型|描述|  
| --- | --- | --- |  
|trade_date|str|交易日期，日期格式为`'yyyy-MM-dd'`|  

__输出参数__:

|名称|类型|描述|  
|----|---|---|  
|output|dataframe|交易日停复牌数据|  

## 财务数据

### 利润表

接口：`get_income`  
描述：返回利润表数据  
__输入参数__： 

|名称|类型|描述|  
| --- | --- | --- |  
|stock_code|list/str|股票代码，例如'000001'或股票代码列表；可选项，默认为全部股票|  
|end_date|str|季末日期，日期格式为`'yyyy-MM-dd'`；end_date和(from_date,end_date)二选其一，可分别获取单日/周期内利润表数据|  
|from_date|str|起始日期，日期格式为`'yyyy-MM-dd'`|  
|end_date|str|终止日期，日期格式为`'yyyy-MM-dd'`|  

__输出参数__:

|名称|类型|描述|  
|----|---|---|  
|output|dataframe|指定股票代码的季度利润表数据|  


### 资产负债表

接口：`get_balancesheet`  
描述：返回资产负债表数据  
__输入参数__： 

|名称|类型|描述|  
| --- | --- | --- |  
|stock_code|list/str|股票代码，例如'000001'或股票代码列表；可选项，默认为全部股票|  
|end_date|str|季末日期，日期格式为`'yyyy-MM-dd'`；end_date和(from_date,end_date)二选其一，可分别获取单日/周期内资产负债表数据|  
|from_date|str|起始日期，日期格式为`'yyyy-MM-dd'`|  
|end_date|str|终止日期，日期格式为`'yyyy-MM-dd'`|  

__输出参数__:

|名称|类型|描述|  
|----|---|---|  
|output|dataframe|指定股票代码的季度资产负债表数据|  


### 现金流量表

接口：`get_cashflow`  
描述：返回现金流量表数据  
__输入参数__： 

|名称|类型|描述|  
| --- | --- | --- |  
|stock_code|list/str|股票代码，例如'000001'或股票代码列表；可选项，默认为全部股票|  
|end_date|str|季末日期，日期格式为`'yyyy-MM-dd'`；end_date和(from_date,end_date)二选其一，可分别获取单日/周期内现金流量表数据|  
|from_date|str|起始日期，日期格式为`'yyyy-MM-dd'`|  
|end_date|str|终止日期，日期格式为`'yyyy-MM-dd'`|  

__输出参数__:

|名称|类型|描述|  
|----|---|---|  
|output|dataframe|指定股票代码的季度现金流量表数据|  


### 财务指标

接口：`get_fina_indicator`  
描述：返回财务指标数据  
__输入参数__： 

|名称|类型|描述|  
| --- | --- | --- |  
|stock_code|list/str|股票代码，例如'000001'或股票代码列表；可选项，默认为全部股票|  
|end_date|str|季末日期，日期格式为`'yyyy-MM-dd'`，end_date和(from_date,end_date)二选其一，可分别获取单日/周期内财务指标数据|  
|from_date|str|起始日期，日期格式为`'yyyy-MM-dd'`|  
|end_date|str|终止日期，日期格式为`'yyyy-MM-dd'`|  

__输出参数__:

|名称|类型|描述|  
|----|---|---|  
|output|dataframe|指定股票代码的季度财务指标数据|  

