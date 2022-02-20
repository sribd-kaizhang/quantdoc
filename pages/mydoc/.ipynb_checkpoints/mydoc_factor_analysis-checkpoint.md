---
title: 单因子测试
tags: [single_sourcing]
last_updated: January 21, 2022
keywords: factor analysis
summary: "This page is for elaborating methods of factor analysis."
sidebar: mydoc_sidebar
permalink: mydoc_factor_analysis.html
folder: mydoc
---



__`factor_analysis`是一款基于Python的单因子测试框架，为寻找能有效区分和预测股票收益的因子提供标准化的工作流程和实现工具。该框架主要包括数据清洗与因子测试两部分。其中，数据清洗将实现对原始因子数据中异常值和缺失值的处理，以及因子标准化，从而保证后续检验模型的稳健性；因子测试提供三类因子测试模型，帮助投资者从实证角度验证因子有效性，分别为回归检验、投资组合排序法以及信息系数评估。__

本页主要介绍以上所提到的因子测试模型的函数使用方法。

## Fama-MacBeth回归法

`factor_analysis`类提供` factor_fm_summ`方法，支持Fama-MacBeth回归验证因子。检验因子前，需要指定定价模型（默认为FF-3模型，可选CAPM）。考虑到异方差问题和残差自相关问题，回归系数的标准误将通过Newey-West修正（默认lag = 5）。判断候选因子是否有效需检验该因子是否能在定价模型因子基础上提供增量信息，即检验候选因子在FM回归中斜率系数是否显著不等于0。

__使用样例__

```python
# Fama-MacBeth regression
fa.factor_fm_regr_summ(pricing_model = 'FF-3')
```
其中参数包括:   
__pricing_model__: 可选参数，str, 默认'FF-3'  
&#8195;&#8195;定价模型，其中'FF-3'对应Fama-French三因子模型，'CAPM'对应资本资产定价模型；


## Barra回归法

`factor_analysis`类提供` factor_beta_cs_regr`和`factor_beta_cs_summ`方法，支持Barra回归方法验证因子有效性，包括计算因子每期收益、因子收益率序列t检验、有效因子分类等。单因子回归验证风格因子有效性时，每个换仓期期初的公司特征作为因子暴露，与行业因子（0-1哑变量）和市值因子共同作为回归式的解释变量，换仓期期初至期末的个股收益作为响应变量，以流通市值为权重利用加权最小二乘法回归（WLS）拟合得到的斜率项即为因子在该换仓期的因子收益。在进行因子收益率序列检验时，通过对多期因子收益进行t-检验，将获得t值序列及相关统计指标，从而对因子的有效性、稳定性与方向一致性等性质进行验证。

__使用样例__

```python
# statistics on factor return series 
fa.factor_barra_regr_summ(industry_neutral=True,mkt_cap_neutral=True)
```
其中参数包括:   
__industry_neutral__: 可选参数，bool, 默认True  
&#8195;&#8195;是否考虑行业中性化，若选择True，个股行业因子将以0-1哑变量形式作为解释变量加入到回归式；  
__mkt_cap_neutral__: 可选参数，bool, 默认True  
&#8195;&#8195;是否考虑市值中性化，若选择True，个股市值因子将作为解释变量加入到回归式；  


## 时序回归法

`factor_analysis`类提供` factor_ts_regr_summ()`方法，支持时间序列回归检验因子。回归方程式中，由异象变量（anomaly variables）构建的多空组合收益率将作为被解释变量，指定的定价模型（默认FF-3，可选CAPM，FF-5模型）的因子收益率将作为解释变量，通过对截距项进行t-检验判断异象因子是否有效。t-检验时，考虑到回归式中的残差项的异方差和自相关问题，将通过Newey-West修正标准误估计。其中，在考虑定价模型因子收益率时，可选择剔除科创版与创业板股票（默认包括科创版与创业板），利用Double Sorting方法（默认2×3组合划分方法,可选2×2）与流通市值加权方式计算定价因子收益率。

__使用样例__

```python
# time-series regression
fa.factor_ts_regr_summ(pricing_model='FF-3',kechuangchuangye=True,portfolio_method='2*3')
```

其中参数包括:   
__pricing_model__: 可选参数，str, 默认'FF-3'  
&#8195;&#8195;定价模型，其中'CAPM'对应资本资产定价模型，'FF-3'对应Fama-French三因子模型，'FF-5'对应Fama-French五因子模型；  
__kechuangchuangye__: 可选参数，bool, 默认True  
&#8195;&#8195;定价因子计算收益率时是否考虑科创版与创业板股票，若选择True，将包括科创版与创业板股票，否则则不加入；  
__portfolio_method__: 可选参数，bool, 默认True  
&#8195;&#8195;定价因子计算收益率时Double Sorting多空组合划分方式，若'2×3'，将以FF模型2×3组合划分方法构建多空组合；  


## 因子IC值法

`factor_analysis`类提供` factor_ic_cmpt`和`factor_ic_summ`方法，支持信息系数（Information Coefficient, IC）方法验证因子有效性，包括因子提纯、计算因子IC值、因子IC值序列检验等。在利用IC值评价因子有效性前，`factor_ic_cmpt`默认会预先对因子进行提纯，排除行业、市值等重要因素的影响（可选不进行行业或市值中性，industry_neutral=False，mkt_cap_neutral=False）。在每个截面期上，测试因子作为响应变量对市值因子及行业因子做线性回归，取残差作为测试因子的替代值，即可消除因子在行业、市值等方面的偏离。在计算IC值时，`factor_ic_cmpt`采用更具鲁棒性的秩相关系数（Spearman Rank Correlation）计算每一期初个股因子暴露（剔除行业与市值后）与其到期末的收益率之间的相关性。获取IC值序列后，`factor_ic_summ`方法将用于计算与IC值相关的指标，从而判断因子的有效性和预测能力。

__使用样例__

```python
# statistics on adjusted rank IC series 
fa.factor_ic_summ(industry_neutral=True,mkt_cap_neutral=True)
```
其中参数包括:   
__industry_neutral__: 可选参数，bool, 默认True  
&#8195;&#8195;是否考虑行业中性化，若选择True，候选因子将通过行业变量进行正交或提纯；  
__mkt_cap_neutral__: 可选参数，bool, 默认True  
&#8195;&#8195;是否考虑市值中性化，若选择True，候选银子将通过市值变量进行正交或提纯；  



## 分层回测法

`factor_analysis`类提供` quantile_returns_cmpt`，`quantile_returns_plot`与  `quantile_returns_summ`方法，支持依照因子值对股票进行打分，构建投资组合回测，并应用统计指标与可视化方法评价各投资组合表现。在计算投资组合收益率时，`quantile_returns_cmpt`方法采取流通市值加权方法计算投资组合每期收益率。`quantile_returns_summ`方法将利用t-值、年化收益率、累计收益率、年化波动率、最大回测、夏普比率等指标评价各投资组合在回测区间内的表现。`quantile_return_plot`方法将可视化各投资组合在回测期内的累计收益率曲线。

__使用样例__

```python
fa.quantile_returns_cmpt()
fa.quantile_returns_summ()
fa.quantile_returns_plot(plot_type = 'longshort')
```
其中`quantile_returns_plot`参数包括：
__plot_type__:可选参数，str，默认'longshort'  
&#8195;&#8195;可视化类别，若选择longshort，将可视化top组、buttom组和long-short组的累计收益率曲线；若选择'all_quantiles'，将可视化所有分位数组别的累计收益率曲线；  