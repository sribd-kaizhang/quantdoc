---
title: "Getting started with our quantitative asset management toolkit"
keywords: homepage
tags: [getting_started]
sidebar: mydoc_sidebar
permalink: index.html
summary: These brief instructions will help you get started quickly with the toolkit. The other topics in this help provide additional information and detail about working with other aspects of this toolkit.
---

{% include note.html content="平台仅供政企大数据实验室内部使用" %}

__该平台是深圳市大数据研究院政企大数据实验室量化资管团队开发的基于Python语言的量化因子投资工具箱，包含数据管理、因子计算、单因子分析、策略回测等多个模块，目的是帮助量化多因子策略的开发与测试。__



以下介绍目前平台实现的模块与功能：

* `store_data`与`get_data` - 批量存储、更新与获取行情、财务报表与其他A股有关数据。
* `get_factor` - 计算异象因子及对应公司特征。
* `factor_analysis` - 单因子与多因子测试，包括（横截面与时间序列）回归法、投资组合排序与信息系数计算等。
* ` backtest` - 基于向量化的策略回测框架，支持计算评价指标、绘制收益曲线与生成交易日志等。
