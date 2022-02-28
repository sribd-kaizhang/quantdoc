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

```
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

```
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

**输入参数:**

|名称|必选|类型|描述|
|----|----|----|---|
|`factor`|Y|DataFrame|因子数据，其中二维索引分别为交易日期 *trade_date（level 0）*与股票代码 *stock_code（level 1）*，并包含一个名称为 *factor*的列，其值为对应交易日期、股票代码的因子值|
|`returns`|Y|DataFrame|收益率数据，其中二维索引分别为交易月份 *trade_month（level 0）*与股票代码 *stock_code（level 1）*，并包含一个名称为 *returns*的列，其值为对应交易月份、股票代码的月收益率|
|`quantile`|N|int|投资组合数量，默认为10|
|`outlier_method`|N|str|异常值处理方法，默认'winsorize'，即缩尾法；可选'mad'，即绝对中位差法|
|`norm_method`|N|str|标准化方法，默认'zscore'，即为z-score标准化；可选'rank'，即为基于秩的标准化方法|
|`industry_neutral`|N|bool|按因子值排序分组时，是否行业中性化处理，默认为`False`，即对因子进行行业中性化处理；可选`True`，即不进行行业中性化处理|
|`mkt_cap_neutral`|N|bool|按因子值排序分组时，是否市值中性化处理，默认`False`，即对因子进行市值中性化处理；可选`True`，即不进行市值中性化处理|

**输出参数：**

1. *属性列表：*

|名称|初始|类型|描述|
|----|----|----|---|
|`factor_data`|Y|DataFrame|因子数据，其中二维索引分别为交易日期 *trade_date（level 0）*与股票代码 *stock_code（level 1）*，并包含一个名称为 *factor*的列，其值为对应交易日期、股票代码的原始因子值|
|`returns_data`|Y|DataFrame|收益率数据，其中二维索引分别为交易月份 *trade_month（level 0）*与股票代码 *stock_code（level 1）*，并包含一个名称为 *returns*的列，其值为对应交易月份、股票代码的月收益率|
|`factor_return_data`|Y|DataFrame|进行预处理后的因子与收益率合并数据，其中二维索引分别为交易月份 *trade_month（level 0）*与股票代码*stock_code（level 1）*，并包含名称分别为 *factor*、*returns*、*industry*、*quantiles*、*circ_mc_log* 的列，其值分别为对应交易月份、股票代码的因子值（处理后）、月收益率、所属行业、排序组别、流动市值对数|

2. *方法列表：*

|名称|描述|
|----|---|
|`factor_ts_regr_summ`|回归法检验定价因子是否能在时间序列维度上解释潜在异象因子|
| `factor_fm_regr_summ`    |回归法检验潜在异象因子是否能在已知定价模型的基础上，为解释不同股票的收益率差异提供增量信息|
|`factor_barra_regr_cmpt`|Barra回归计算回测期内每个月的因子收益率与t值|
|`factor_barra_regr_summ`|Barra回归计算回测期内每个月的因子收益率与t值，并在时间序列的维度上计算因子收益率与t值的相关统计指标|
|`factor_ic_cmpt`|信息系数计算回测期内每个月因子与未来收益率的相关性，检验潜在异象因子是否能预测股票的未来收益率|
|`factor_ic_summ`|信息系数计算回测期内每个月因子与未来收益率的相关性，并在时间序列的维度计算可预测性的相关统计指标|
|`quantile_returns_cmpt`|投资组合排序法计算不同因子值大小构建的投资组合在回测期内每个月的收益率|
|`quantile_returns_summ`|投资组合排序法计算不同因子值大小构建的投资组合在回测期内每个月的收益率，并计算描述投资组合回测期内表现的统计指标（如t值、夏普比率、年化收益率、累计收益率等）|
|`quantile_returns_plot`|投资组合排序法计算不同因子值大小构建的投资组合在回测期内每个月的收益率，并绘制投资组合回测内的累计收益率曲线|

## 数据预处理

在测试前，为保证后续检验模型的稳健性，`factor_analysis`将对原始因子数据与收益率数据进行预处理，其中包括以下步骤：

* 剔除高风险股票与不可交易股，包括换仓日前一天的风险警示股、次新股以及停牌股等；

* 缺失值处理，剔除因子值缺失的股票（主要包括过去一段时间交易天数不足的股票，与上市时间不满一年而无法计算TTM指标或去年同比变化指标的股票）；

* 异常值检测，采用固定比率修正法/缩尾法，或MAD检验并修正因子的异常值；

* 数据标准化，采用Z-Score标准化，或基于轶的标准化方法对因子数据进行标准化处理；

* 数据合并，将第$T-1$期末的因子数据与第$T$期的收益率数据进行左连接；

* 补充信息，包括股票行业、流通市值以及根据因子值分位数排序并分组后的结果；

经过预处理后的数据将保存在名称为`factor_return_data`且格式为MultiIndex DataFrame的属性中，其二维索引分别为交易月份 _trade_month（level 0）_与股票代码 _stock_code（level 1）_，列包含交易日期 _trade_date_、因子值 _factor_、个股月收益率 _returns_、2012版证监会行业分类 _industry_、个股流通市值 _circ_mc_ 以及因子分位数组别      _quantiles_。当根据因子值排序构建分位数投资组合时，若考虑进行行业中性化或市值中性化处理，则将行业和（或）市值作为解释变量，以因子值作为被解释变量做回归，所得残差即为中性化后的因子值。

**数据样例：**

```python
fa.factor_return_data
```

```
                        trade_date    factor   returns                    industry       circ_mc quantiles  
trade_month stock_code                                                     
2010-01     000001      2009-12-31  2.202307 -0.109561            货币金融服务        7.126066e+07  group 10 
            000002      2009-12-31  2.540593 -0.135985              房地产业         1.043824e+08  group 10  
            000005      2009-12-31 -0.533783 -0.104651        生态保护和环境治理业     5.500733e+06   group 4  
            000006      2009-12-31 -0.488849 -0.120918              房地产业         5.589346e+06   group 4  
            000009      2009-12-31  0.277774 -0.050091                综合          1.084956e+07   group 8  
...                            ...       ...       ...               ...   
2021-11     688699      2021-10-29  0.112618  0.031083        软件和信息技术服务业     3.744605e+06   group 7  
            688777      2021-10-29  1.060265  0.021838        软件和信息技术服务业     3.616792e+06   group 9  
            688788      2021-10-29 -0.332742  0.105668  计算机、通信和其他电子设备制造业  6.079314e+06   group 5  
            688819      2021-10-29  0.997068  0.187730        电气机械及器材制造业     4.328712e+06   group 9  
            688981      2021-10-29  1.948281 -0.014172  计算机、通信和其他电子设备制造业  1.029819e+08  group 10 

[193210 rows x 6 columns]
```