---
title: 异象因子接口
tags: [single_sourcing]
last_updated: February 11, 2022
keywords: factor description
summary: "This page provides the functions to compute the anomaly factors."
sidebar: mydoc_sidebar
permalink: mydoc_factor_function.html
folder: mydoc
---

__因子库`factor_library`提供包括交易摩擦因子（市值因子、波动率因子、高阶距因子、流动性因子、Beta因子）、动量因子、价值因子、成长因子、盈利因子与财务流动性因子等六大类因子对应公司特征数据，本部分将针对每类因子的数据接口进行描述。__

调用因子库前，需要导入`factor_library`模块：

```python
from factors_library import get_factors as gf
```

## 市值因子

接口：`get_size_factor`  
描述：根据指定日期，返回市值特征。当输入单个日期时（_trade_date_），函数返回输入日期前最后一个交易日盘后数据；当输入日期区间（_from_date_与_to_date_），函数返回输入日期区间内每月最后一个交易日盘后数据；

__输入参数__：  

|名称 |类型 |必选 |描述 |  
| --- | --- | --- | --- |
|`from_date`|str|N|起始日期，日期格式为`'yyyy-MM-dd'`|  
|`to_date`|str|N|终止日期，日期格式为`'yyyy-MM-dd'`| 
|`trade_date`|str|N|交易日期，日期格式为`'yyyy-MM-dd'`|

__输出参数__:

|名称 |类型 |描述 |
| --- |--- |--- |
|`trade_date`|str|交易日期|
|`stock_code`|str|股票代码|
|`mc`|float|总市值|
|`mc_log`|float|总市值对数|
|`circ_mc`|float|流动市值|
|`circ_mc_log`|float|流动市值对数|
|`mc_nonlinear`|float|非线性市值|
|`circ_to_total_mc_ratio`|float|流通市值占总市值比重|



## 波动率因子

接口：`get_volatility_factor`  
描述：根据指定日期，返回波动率特征。当输入单个日期时（_trade_date_），函数返回输入日期前最后一个交易日盘后数据；当输入日期区间（_from_date_与_to_date_），函数返回输入日期区间内每月最后一个交易日盘后数据；

__输入参数__：  

|名称 |类型 |必选 |描述 |  
| --- | --- | --- | --- |
|`from_date`|str|N|起始日期，日期格式为`'yyyy-MM-dd'`|  
|`to_date`|str|N|终止日期，日期格式为`'yyyy-MM-dd'`| 
|`trade_date`|str|N|交易日期，日期格式为`'yyyy-MM-dd'`|

__输出参数__:

|名称 |类型 |描述 |
| --- |--- |--- |
|`trade_date`|str|交易日期|
|`stock_code`|str|股票代码|
|`vol_1m`|float|1个月日收益率波动率|
|`vol_1y`|float|12个月日收益率波动率|
|`ido_vol_1m`|float|1个月异质波动率|
|`ido_vol_1y`|float|12个月异质波动率|
|`skew`|float|偏态|
|`ido_skew`|float|异质偏态|
|`con_skew`|float|条件偏态|
|`ret_max`|float|1个月最大日收益率|

## 流动性因子

接口：`get_liquidity_factor`  
描述：根据指定日期，返回流动性特征。当输入单个日期时（_trade_date_），函数返回输入日期前最后一个交易日盘后数据；当输入日期区间（_from_date_与_to_date_），函数返回输入日期区间内每月最后一个交易日盘后数据；

__输入参数__：  

|名称 |类型 |必选 |描述 |  
| --- | --- | --- | --- |
|`from_date`|str|N|起始日期，日期格式为`'yyyy-MM-dd'`|  
|`to_date`|str|N|终止日期，日期格式为`'yyyy-MM-dd'`| 
|`trade_date`|str|N|交易日期，日期格式为`'yyyy-MM-dd'`|

__输出参数__:

|名称 |类型 |描述 |
| --- |--- |--- |
|`trade_date`|str|交易日期|
|`stock_code`|str|股票代码|
|`turn_1m`|float|1个月日换手率|
|`turn_std_1m`|float|1个月日换手率波动率|
|`turn_1y`|float|12个月日换手率|
|`turn_std_1y`|float|12个月日换手率波动率|
|`turn_abn`|float|异常换手率|
|`illiq_1m`|float|1个月非流动性|
|`illiq_1y`|float|12个月非流动性|

## Beta因子

接口：`get_beta_factor`  
描述：根据指定日期，返回Beta系数/系统性风险特征。当输入单个日期时（_trade_date_），函数返回输入日期前最后一个交易日盘后数据；当输入日期区间（_from_date_与_to_date_），函数返回输入日期区间内每月最后一个交易日盘后数据；

__输入参数__：  

|名称 |类型 |必选 |描述 |  
| --- | --- | --- | --- |
|`from_date`|str|N|起始日期，日期格式为`'yyyy-MM-dd'`|  
|`to_date`|str|N|终止日期，日期格式为`'yyyy-MM-dd'`| 
|`trade_date`|str|N|交易日期，日期格式为`'yyyy-MM-dd'`|

__输出参数__:

|名称 |类型 |描述 |
| --- |--- |--- |
|`trade_date`|str|交易日期|
|`stock_code`|str|股票代码|
|`beta`|float|系统性风险|
|`beta_up`|float|上行风险|
|`beta_down`|float|下行风险|
|`beta_relative`|float|上行风险/下行风险|
|`dimson`|float|Dimson Beta系数|

## 动量反转因子

接口：`get_momentum_factor`  
描述：根据指定日期，返回动量（反转）特征。当输入单个日期时（_trade_date_），函数返回输入日期前最后一个交易日盘后数据；当输入日期区间（_from_date_与_to_date_），函数返回输入日期区间内每月最后一个交易日盘后数据；

__输入参数__：  

|名称 |类型 |必选 |描述 |  
| --- | --- | --- | --- |
|`from_date`|str|N|起始日期，日期格式为`'yyyy-MM-dd'`|  
|`to_date`|str|N|终止日期，日期格式为`'yyyy-MM-dd'`| 
|`trade_date`|str|N|交易日期，日期格式为`'yyyy-MM-dd'`|

__输出参数__:

|名称 |类型 |描述 |
| --- |--- |--- |
|`trade_date`|str|交易日期|
|`stock_code`|str|股票代码|
|`mom_1m`|float|1个月动量/短期反转|
|`mom_6m`|float|6个月动量|
|`mom_12m`|float|12个月动量|
|`ido_mom`|float|异质动量|
|`mom_chg`|float|动量变化|

## 价值因子

接口：`get_value_factor`  
描述：根据指定日期，返回价值特征。当输入单个日期时（_trade_date_），函数返回输入日期前最后一个交易日盘后数据；当输入日期区间（_from_date_与_to_date_），函数返回输入日期区间内每月最后一个交易日盘后数据；

__输入参数__：  

|名称 |类型 |必选 |描述 |  
| --- | --- | --- | --- |
|`from_date`|str|N|起始日期，日期格式为`'yyyy-MM-dd'`|  
|`to_date`|str|N|终止日期，日期格式为`'yyyy-MM-dd'`| 
|`trade_date`|str|N|交易日期，日期格式为`'yyyy-MM-dd'`|

__输出参数__:

|名称 |类型 |描述 |
| --- |--- |--- |
|`trade_date`|str|交易日期|
|`stock_code`|str|股票代码|
|`bm`|float|账面市值比|
|`am`|float|总资产市值比|
|`lm`|float|总负债市值比|
|`ep`|float|收益价格比|
|`cfp`|float|现金流价格比|
|`ocfp`|float|营业现金流价格比|
|`dp`|float|股利价格比|
|`sp`|float|营业收入价格比|


## 成长因子

接口：`get_growth_factor`  
描述：根据指定日期，返回成长特征。当输入单个日期时（_trade_date_），函数返回输入日期前最后一个交易日盘后数据；当输入日期区间（_from_date_与_to_date_），函数返回输入日期区间内每月最后一个交易日盘后数据；

__输入参数__：  

|名称 |类型 |必选 |描述 |  
| --- | --- | --- | --- |
|`from_date`|str|N|起始日期，日期格式为`'yyyy-MM-dd'`|  
|`to_date`|str|N|终止日期，日期格式为`'yyyy-MM-dd'`| 
|`trade_date`|str|N|交易日期，日期格式为`'yyyy-MM-dd'`|

__输出参数__:

|名称 |类型 |描述 |
| --- |--- |--- |
|`trade_date`|str|交易日期|
|`stock_code`|str|股票代码|
|`asset_g`|float|总资产增长率|
|`liab_g`|float|总负债增长率|
|`bm_g`|float|净资产增长率|
|`sales_g_ttm`|float|营业收入增长率（TTM）|
|`sales_g_q`|float|营业收入增长率（季度）|
|`gm_g_ttm`|float|营业利润增长率（TTM）|
|`gm_g_q`|float|营业利润增长率（季度）|
|`profit_g_ttm`|float|净利润增长率（TTM）|
|`profit_g_q`|float|净利润增长率（季度）|
|`inv_g`|float|存货增长率|
|`income_tax_g_ttm`|float|所得税增长率（TTM）|
|`income_tax_g_q`|float|所得税增长率（季度）|
|`acc`|float|增值因子|
|`acc_abs`|float|增值因子绝对值|
|`eq_g`|float|所有股东权益（不包含少数股东）变化率|
|`noa`|float|净经营资产|
|`sales_g_minus_inv_g`|float|营业收入变化减存货净额变化|
|`sales_g_minus_ar_g`|float|营业收入变化减应收账款变化|
|`sales_g_minus_sga_g`|float|营业收入变化三费支出变化|
|`rd`|float|研发支出|
|`rd_to_mc`|float|研发支出市值比|
|`rd_to_sales`|float|研发支出收入比|


## 盈利因子

接口：`get_profit_factor`  
描述：根据指定日期，返回盈利能力特征。当输入单个日期时（_trade_date_），函数返回输入日期前最后一个交易日盘后数据；当输入日期区间（_from_date_与_to_date_），函数返回输入日期区间内每月最后一个交易日盘后数据；

__输入参数__：  

|名称 |类型 |必选 |描述 |  
| --- | --- | --- | --- |
|`from_date`|str|N|起始日期，日期格式为`'yyyy-MM-dd'`|  
|`to_date`|str|N|终止日期，日期格式为`'yyyy-MM-dd'`| 
|`trade_date`|str|N|交易日期，日期格式为`'yyyy-MM-dd'`|

__输出参数__:

|名称 |类型 |描述 |
| --- |--- |--- |
|`trade_date`|str|交易日期|
|`stock_code`|str|股票代码|
|`roe_q`|float|净资产收益率（季度）|
|`roe_ttm`|float|净资产收益率（TTM）|
|`roa_q`|float|总资产收益率（季度）|
|`roa_ttm`|float|总资产收益率（TTM）|
|`gp_q`|float|毛利率（季度）|
|`gp_ttm`|float|毛利率（TTM）|
|`ct`|float|资本换手率|
|`pa`|float|利润资产比率|
|`op`|float|营业利润率|
|`gm_chg_minu_sales_chg`|float|毛利率变化减营业收入变化|
|`roic_q`|float|投入资本回报率（季度）|
|`roic_ttm`|float|投入资本回报率（TTM）|

## 财务流动性因子

接口：`get_fina_liq_factor`  
描述：根据指定日期，返回财务流动性特征。当输入单个日期时（_trade_date_），函数返回输入日期前最后一个交易日盘后数据；当输入日期区间（_from_date_与_to_date_），函数返回输入日期区间内每月最后一个交易日盘后数据；

__输入参数__：  

|名称 |类型 |必选 |描述 |  
| --- | --- | --- | --- |
|`from_date`|str|N|起始日期，日期格式为`'yyyy-MM-dd'`|  
|`to_date`|str|N|终止日期，日期格式为`'yyyy-MM-dd'`| 
|`trade_date`|str|N|交易日期，日期格式为`'yyyy-MM-dd'`|

__输出参数__:

|名称 |类型 |描述 |
| --- |--- |--- |
|`trade_date`|str|交易日期|
|`stock_code`|str|股票代码|
|`curr`|float|流动比率|
|`quick`|float|速动比率|
|`cf_to_debt`|float|现金流负债比率|
|`sales_to_cash`|float|营业收入现金比|
|`curr_g`|float|流动比率增长率|
|`quick_g`|float|速动比率增长率|
|`sales_to_inv_g`|float|营业收入存货比增长率|
|`sales_to_receiv`|float|营业收入应收账款比|
|`tang`|float|偿债能力|