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
描述：根据交易频率，筛选指定时段交易日  
输入参数：  

|位置|名称|类型|描述|  
|:-:|:-:|:-:|:-:|  
|输入|from_date|str|起始日期，例如'2022-01-01'|  
|输入|end_date|str|终止日期，例如'2022-01-01'| 
|输入|freq|str|频率，其中包括stock_code列|  
|输入|stock_code|list|股票代码列表，股票代码例为'000001'|  
|输出|df|dataframe|指定股票代码的数据集|  

### 行业分类

接口：`get_industry`  
描述：返回行业分类数据
输入参数：  

|位置|名称|类型|描述|  
|:-:|:-:|:-:|:-:|  
|输入|industry_type|str|分类标准，默认为证监会，可选‘shenwan’|  
|输出|industry_data|dataframe|行业分类数据|  


### 风险警示股

接口：`get_st_stocks`  
描述：返回日频ST股票数据  
输入参数：  

|位置|名称|类型|描述|  
|:-:|:-:|:-:|:-:|  
|输入|trade_date|str|交易日期，例如'2022-01-01'|  
|输出|st_list|list|交易日停复牌数据|  

### 新上市股票

接口：`get_new_stocks_code`  
描述：返回新上市股票代码  
输入参数：  

|位置|名称|类型|描述|  
|:-:|:-:|:-:|:-:|  
|输入|trade_date|str|交易日期，例如'2022-01-01'|  
|输入|days|int|天数，指定当日前N天|  
|输出|new_stock+cdr|list|周期内新上市股票代码|  

* 获取周期内季末日期

接口：`get_quarters`  
描述：根据起止日期，筛选周期内期末日期  
输入参数：  

|位置|名称|类型|描述|  
|:-:|:-:|:-:|:-:|  
|输入|from_date|str|起始日期，例如'2022-01-01'|  
|输入|end_date|str|终止日期，例如'2022-01-01'|  
|输出|Quarter_list|list|周期内所有季末日期|  


* 获取非流动股票数据

接口：`get_illiq_stocks`  
描述：返回日频非流动股票数据  
输入参数：  

|位置|名称|类型|描述|  
|:-:|:-:|:-:|:-:|  
|输入|trade_date|str|交易日期，例如'2022-01-01'|  
|输出|illiq_stocks|dataframe|交易日非流动股票数据|  


## 行情数据

### 日线行情

接口：`get_stocks_daily`  
描述：返回股票日频行情数据
输入参数：  

|位置|名称|类型|描述|  
|:-:|:-:|:-:|:-:|  
|输入|stock_code|list/str|股票代码，形如'000001'，以指定特定股票数据或股票代码列表|  
|输入|trade_date|str|交易日期，例如'2022-01-01'|  
|输入|from_date|str|起始日期，例如'2022-01-01'|  
|输入|end_date|str|终止日期，例如'2022-01-01'|  
|输入|pool|str|股票池，包括'all_a_market','hushen300','zhongzheng500','liquid_perc70'|
|输出|output|dataframe|指定股票代码的日行情数据|  

stock_code为可选项，默认为全部股票；trade_date和(from_date,end_date)二选其一，可分别获取单日/周期内股票日线行情数据；股票池为可选项，默认为全部A股

### 月线行情

接口：`get_stocks_monthly`  
描述：返回股票月频行情数据
输入参数：  

|位置|名称|类型|描述|  
|:-:|:-:|:-:|:-:|  
|输入|stock_code|list/str|股票代码，例如'000001'，以指定特定股票数据或股票代码列表|  
|输入|trade_date|str|交易日期，例如'2022-01-01'|  
|输入|from_date|str|起始日期，例如'2022-01-01'|  
|输入|end_date|str|终止日期，例如'2022-01-01'|  
|输出|output|dataframe|指定股票代码的月行情数据|  

stock_code为可选项，默认为全部股票；trade_date和(from_date,end_date)二选其一，可分别获取单日/周期内股票月线行情数据。  

### 每日指标

接口：`get_daily_basic`  
描述：返回股票日频指标数据  
输入参数：  

|位置|名称|类型|描述|  
|:-:|:-:|:-:|:-:|  
|输入|trade_date|str|交易日期，例如'2022-01-01'|  
|输入|from_date|str|起始日期，例如'2022-01-01'|  
|输入|end_date|str|终止日期，例如'2022-01-01'|  
|输出|output|dataframe|交易日指标数据|  

### 停复牌信息

接口：`get_daily_suspended`  
描述：返回股票日频停复牌数据  
输入参数：  

|位置|名称|类型|描述|  
|:---:|:-----:|:-----:|:--------:|  
|输入|trade_date|str|交易日期，例如'2022-01-01'|  
|输出|output|dataframe|交易日停复牌数据|  

## 财务数据

### 利润表

接口：`get_income`  
描述：返回利润表数据  
输入参数：  

|位置|名称|类型|描述|  
|:-:|:-:|:-:|:-:|  
|输入|stock_code|list/str|股票代码，例如'000001'或股票代码列表|  
|输入|end_date|str|季末日期，例如'2022-01-01'|  
|输入|from_date|str|起始日期，例如'2022-01-01'|  
|输入|end_date|str|终止日期，例如'2022-01-01'|  
|输出|output|dataframe|指定股票代码的季度利润表数据|  

stock_code为可选项，默认为全部股票，trade_date和(from_date,end_date)二选其一，可分别获取单日/周期内利润表数据。  

### 资产负债表

接口：`get_balancesheet`  
描述：返回资产负债表数据  
输入参数：  

|位置|名称|类型|描述|  
|:-:|:-:|:-:|:-:|  
|输入|stock_code|list/str|股票代码，例如'000001'或股票代码列表|  
|输入|end_date|str|季末日期，例如'2022-01-01'|  
|输入|from_date|str|起始日期，例如'2022-01-01'|  
|输入|end_date|str|终止日期，例如'2022-01-01'|  
|输出|output|dataframe|指定股票代码的季度资产负债表数据|  

stock_code为可选项，默认为全部股票，trade_date和(from_date,end_date)二选其一，可分别获取单日/周期内资产负债表数据。  

### 现金流量表

接口：`get_cashflow`  
描述：返回现金流量表数据  
输入参数：  

|位置|名称|类型|描述|  
|:-:|:-:|:-:|:-:|  
|输入|stock_code|list/str|股票代码，例如'000001'或股票代码列表|  
|输入|end_date|str|季末日期，例如'2022-01-01'|  
|输入|from_date|str|起始日期，例如'2022-01-01'|  
|输入|end_date|str|终止日期，例如'2022-01-01'|  
|输出|output|dataframe|指定股票代码的季度现金流量表数据|  

stock_code为可选项，默认为全部股票，trade_date和(from_date,end_date)二选其一，可分别获取单日/周期内现金流量表数据。  

### 财务指标

接口：`get_fina_indicator`  
描述：返回财务指标数据  
输入参数：  

|位置|名称|类型|描述|  
|:-:|:-:|:-:|:-:|  
|输入|stock_code|list/str|股票代码，例如'000001'或股票代码列表|  
|输入|end_date|str|季末日期，例如'2022-01-01'|  
|输入|from_date|str|起始日期，例如'2022-01-01'|  
|输入|end_date|str|终止日期，例如'2022-01-01'|  
|输出|output|dataframe|指定股票代码的季度财务指标数据|  

stock_code为可选项，默认为全部股票，trade_date和(from_date,end_date)二选其一，可分别获取单日/周期内财务指标数据。 




* 获取指数日线行情数据

接口：`get_index_daily`  
描述：返回股票日频行情数据
输入参数：  

|位置|名称|类型|描述|  
|:-:|:-:|:-:|:-:|  
|输入|index_code|str|指数代码，以指定特定指数数据|   
|输入|from_date|str|起始日期，例如'2022-01-01'|  
|输入|end_date|str|终止日期，例如'2022-01-01'|  
|输出|index_data|dataframe|指定指数代码的日行情数据|  

* 获取指数月线行情数据

接口：`get_index_monthly`  
描述：返回指数月频行情数据
输入参数：  

|位置|名称|类型|描述|  
|:-:|:-:|:-:|:-:|  
|输入|index_code|str|指数代码，以指定特定指数数据|   
|输入|from_date|str|起始日期，例如'2022-01-01'|  
|输入|end_date|str|终止日期，例如'2022-01-01'|  
|输出|index_data|dataframe|指定指数代码的日行情数据|  

* 获取新上市股票代码

接口：`get_new_stocks_code`  
描述：返回新上市股票代码  
输入参数：  

|位置|名称|类型|描述|  
|:-:|:-:|:-:|:-:|  
|输入|trade_date|str|交易日期，例如'2022-01-01'|  
|输入|days|int|天数，指定当日前N天|  
|输出|new_stock+cdr|list|周期内新上市股票代码|  
 

* 获取定价模型因子收益率(日)

接口：`get_factor_pricing_model`  
描述：返回定价模型因子日收益率  
输入参数：  

|位置|名称|类型|描述|  
|:-:|:-:|:-:|:-:|  
|输入|pricing_model|str|定价模型，默认为'FF-3'，可取'FF-5'|  
|输入|freq|str|频率，默认为日频，可取'month'|  
|输入|kechuangye|boolean|股票类型，默认包括科创板与创业板|  
|输入|portfolio_method|str|投资组合类型，默认为'2\*3'，可取'2\*2'或'2\*2\*2\*2'|  
|输出|model|dataframe|指定因子收益率数据|  

* 获取定价模型因子变量

接口：`get_factor_pricing_variable`  
描述：返回定价模型因子变量  
输入参数：  

|位置|名称|类型|描述|  
|:-:|:-:|:-:|:-:|  
|输入|pricing_model|str|定价模型，默认为'FF-3'，可取'CAPM'|  
|输出|fa_pr_var|dataframe|指定因子变量|  

* 获取无风险收益率

接口：`get_risk_free_rate`  
描述：返回无风险收益率
输入参数：  

|位置|名称|类型|描述|  
|:-:|:-:|:-:|:-:|  
|输出|rfr_data|dataframe|无风险收益率数据|

* 获取市场收益率

接口：`get_mkt_ret`  
描述：返回市场收益率
输入参数：  

|位置|名称|类型|描述|  
|:-:|:-:|:-:|:-:|  
|输出|mkt_ret|dataframe|市场收益率数据|

* 获取股票池

接口：`get_stocks_pool`  
描述：返回股票池
输入参数：  

|位置|名称|类型|描述|  
|:-:|:-:|:-:|:-:|  
|输入|trade_date|str|交易日期，例如'2022-01-01'|  
|输入|from_date|str|起始日期，例如'2022-01-01'|  
|输入|end_date|str|终止日期，例如'2022-01-01'|  
|输入|pool|str|股票池，默认为'hushen300'，可为'zhongzheng500','liquid_perc70'|
|输出|stocks_pool|dataframe|交易日股票池数据|  