---
title: 因子预处理
tags: [single_sourcing]
last_updated: January 21, 2022
keywords: factor analysis
summary: "This page is for pre-processing step of factor analysis."
sidebar: mydoc_sidebar
permalink: mydoc_factor_analysis_prepare.html
folder: mydoc
---



__单因子测试框架`factor_analysis`主要针对评估单因子有效性问题，支持包括回归法、因子IC值法与多空组合回测法等三类评估方法，通过判断因子值与收益率的相关性，帮助投资者从实证角度验证因子有效性。本页主要介绍`factor_analysis`类的使用方法，以及因子测试前的预处理步骤。__


## 模块导入

单因子测试前，需要导入`factor_analysis`模块。

```python
import factor_analysis as fa
```

## FA类应用

模块`factor_analysis`提供`factor_analysis()`类，其中包含`factor_data`、`returns_data`与`factor_return_data`等多个属性，以及`factor_ts_regr_cmpt()`、`factor_fm_regr_cmpt()`与`quantile_returns_cmpt()`等多种单因子测试方法。`factor_analysis()`类接口调用命令如下：

```python
fa.factor_analysis(
    factors,
    returns,
    quantiles=10,
    outlier_method='winsorize',
    norm_method='zscore',
    industry_neutral=False,
    mkt_cap_neutral=False
)
```

其中参数包括:   
__factors__: 必选参数，MultiIndex DataFrame  
&#8195;&#8195;因子数据，其中二维索引分别为交易日期trade_date（level 0）与股票代码stock_code（level 1），并包含一列factor存储对应交易日期、股票代码的因子值;  
__returns__: 必选参数，MultiIndex DataFrame    
&#8195;&#8195;收益率数据，其中二维索引分别为交易月份trade_month（level 0）与股票代码stock_code（level 1），并包含一列returns存储对应交易月份、股票代码的收益率；  
__quantile__: 可选参数, int，默认为10  
&#8195;&#8195;分组组数，在时间截面水平下将股票按照因子值大小划分为对应数目的组合；  
__outlier_method__: 可选参数，str，默认为'winsorize'  
&#8195;&#8195;异常值处理方法，其中'winsorize'对应缩尾法，'mad'对应绝对中位差法；  
__norm_method__: 可选参数，str，默认为'zscore'  
&#8195;&#8195;标准化方法，其中'zscore'对应z-score标准化方法，'rank'对应rank标准化方法；  
__industry_neutral__: 可选参数，bool，默认为'False'  
&#8195;&#8195;按因子分位数分组时，是否考虑行业中性化；  
__mkt_cap_neutral__: 可选参数，bool，默认为'False'  
&#8195;&#8195;按因子分位数分组时，是否考虑市值中性化；  


## 数据清洗

`factor_analysis`类内部提供数据预处理方法，包括样本筛选（剔除风险警示股票，停牌股，次新股等）、异常值处理、缺失值填充与因子标准化等，同时补充股票行业（industry）、流通市值（circ_mc_log）以及根据因子值分位数排序后的分组结果，经过预处理后的数据保存在`factor_return_data`属性。`factor_return_data`格式为MultiIndex DataFrame，其中二维索引分别为交易月份trade_month（level 0）与股票代码stock_code（level 1），列包含交易日期trade_date、因子值factor、个股月收益率returns、2012版证监会行业分类industry、个股流通市值circ_mc以及因子分位数组别。列trade_date为因子计算时点，个股月收益率returns为该股下月月收益率，circ_mc等于股票trade_date收盘价乘流通市值股数。

```python
fa.factor_return_data
```

```python
                        trade_date    factor   returns          industry  \
trade_month stock_code                                                     
2010-01     000001      2009-12-31  2.202307 -0.109561            货币金融服务   
            000002      2009-12-31  2.540593 -0.135985              房地产业   
            000005      2009-12-31 -0.533783 -0.104651        生态保护和环境治理业   
            000006      2009-12-31 -0.488849 -0.120918              房地产业   
            000009      2009-12-31  0.277774 -0.050091                综合   
...                            ...       ...       ...               ...   
2021-11     688699      2021-10-29  0.112618  0.031083        软件和信息技术服务业   
            688777      2021-10-29  1.060265  0.021838        软件和信息技术服务业   
            688788      2021-10-29 -0.332742  0.105668  计算机、通信和其他电子设备制造业   
            688819      2021-10-29  0.997068  0.187730        电气机械及器材制造业   
            688981      2021-10-29  1.948281 -0.014172  计算机、通信和其他电子设备制造业   

                             circ_mc quantiles  
trade_month stock_code                          
2010-01     000001      7.126066e+07  group 10  
            000002      1.043824e+08  group 10  
            000005      5.500733e+06   group 4  
            000006      5.589346e+06   group 4  
            000009      1.084956e+07   group 8  
...                              ...       ...  
2021-11     688699      3.744605e+06   group 7  
            688777      3.616792e+06   group 9  
            688788      6.079314e+06   group 5  
            688819      4.328712e+06   group 9  
            688981      1.029819e+08  group 10  

[193210 rows x 6 columns]
```