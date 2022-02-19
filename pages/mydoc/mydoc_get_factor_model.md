---
title: 因子模型
tags: [single_sourcing]
last_updated: February 16, 2022
keywords: data management
summary: "This page is for data of factor models."
sidebar: mydoc_sidebar
permalink: mydoc_get_factor_model.html
folder: mydoc
---


## 因子模型

### 定价模型因子收益率

接口：`get_factor_pricing_model`  
描述：获取定价模型因子的日收益率  
__输入参数__：  

|名称|类型|描述|  
|---|---|---|  
|`pricing_model`|str|定价模型，默认为'FF-3'，即'Fama-French'三因子模型；可选'FF-5'，即'Fama-French'五因子模型|  
|`freq`|str|频率，默认为'daily'，即日频；可选'monthly'，即月频|  
|`kechuangye`|bool|是否包括科创版与创业板，默认`True`,可选`False`|  
|`portfolio_method`|str|投资组合类型，默认为'2*3'，代表2*3投资组合划分方法；可选'2*2'，代表2*2投资组合划分方法；可选'2*2*2*2'，代表2*2*2*2投资组合划分方法|  

__输出参数__:

|名称|类型|描述|
|----|----|----| 
|`trade_date`|str|交易日期|
|`RiskPremium`|float|市场风险溢价因子|
|`SMB`|float|市值因子|
|`HML`|float|账面市值比因子|
|`RMW`|float|盈利能力因子|
|`CMA`|float|投资模式因子|

### 定价模型公司特征

接口：`get_factor_pricing_variable`  
描述：获取一段时期内定价模型在每个月最后一个交易日的公司特征  
__输入参数__：  

|名称|类型|描述|  
|----|----|----|  
|`pricing_model`|str|定价模型，默认为'FF-3'，即'Fama-French'三因子模型；可取'CAPM'，即资本资产定价模型|  
|输出|fa_pr_var|dataframe|指定因子变量|  

__输出参数__"
|名称|类型|描述|  
|----|----|----| 
|`trade_date`|str|交易日期|
|`stock_code`|str|股票代码|
|`beta`|float|系统性风险|
|`circ_mc_log`|float|流动市值|
|`ep_ttm`|float|收益价格比|
