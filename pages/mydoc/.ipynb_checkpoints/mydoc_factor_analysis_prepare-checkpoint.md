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



__`factor_analysis`是一款基于Python的单因子测试框架，为寻找能有效区分和预测股票收益的因子提供标准化的工作流程和实现工具。该框架主要包括数据清洗与因子测试两部分。其中，数据清洗将实现对原始因子数据中异常值和缺失值的处理，以及因子标准化，从而保证后续检验模型的稳健性；因子测试提供三类因子测试模型，帮助投资者从实证角度验证因子有效性，分别为回归检验、投资组合排序法以及信息系数评估。__

本页主要介绍使用框架前的数据准备、fa类的使用与结构，以及数据清洗的具体内容。

## 数据准备

首先，导入`factor_analysis`模块。

```python
import factor_analysis as fa
```
在使用`factor_analysis`之前，需要准备好因子数据与收益率数据。其中因子数据需要处理成 _pandas.DataFrame_ 格式，且其二维索引必须为交易日期(_trade_date_)和股票代码(_stock_code_)；收益率数据同样需要处理成 _pandas.DataFrame_ 格式，其二维索引必须为交易月份(_trade_month_)和股票代码（_stock_code_）。

### 因子数据

使用样例:

```python
                            factor
trade_date stock_code
2009-12-31 000001     7.567942e+07
           000002     1.046436e+08
           000005     5.504288e+06
           000006     5.746386e+06
           000009     1.197644e+07
...                            ...
2021-10-29 688779     4.516272e+07
           688798     3.552566e+07
           688819     3.961308e+07
           688981     1.066930e+08
           689009     4.510006e+06
```

### 收益率数据

使用样例:

```python
                       close
trade_month ts_code          
2010-01     000001    13.930
            000002    13.120
            000005    17.350
            000006     6.500
            000007    14.460
...                      ...
2021-11     900948     0.867
            900952     0.239
            900953     0.341
            900955     0.126
            900957     0.635
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

__输入参数__:

|名称|必选|类型|描述|
|----|----|----|---|
|factor|Y|DataFrame|因子数据，其中二维索引分别为交易日期trade_date（level 0）与股票代码stock_code（level 1），并包含一个名称为factor的列，其值为对应交易日期、股票代码的因子值|
|returns|Y|DataFrame|收益率数据，其中二维索引分别为交易月份trade_month（level 0）与股票代码stock_code（level 1），并包含一个名称为returns的列，其值为对应交易月份、股票代码的月收益率|
|quantile|N|int|投资组合数量，默认为10|
|outlier_method|N|str|异常值处理方法，默认'winsorize'，即缩尾法；可选'mad'，即绝对中位差法|
|norm_method|N|str|标准化方法，默认'zscore'，即为z-score标准化；可选'rank'，即为基于秩的标准化方法|
|industry_neutral|N|bool|是否行业中性化处理，默认为`False`，即对因子进行行业中性化处理；可选`True`，即不进行行业中性化处理|
|mkt_cap_neutral|N|bool|是否市值中性化处理，默认`False`，即对因子进行市值中性化处理；可选`True`，即不进行市值中性化处理|

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