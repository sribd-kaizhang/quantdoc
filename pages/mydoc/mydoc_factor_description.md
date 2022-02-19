---
title: 异象因子描述
tags: [single_sourcing]
last_updated: February 11, 2022
keywords: factor description
summary: "This page describes the anomaly factors and their computing methods."
sidebar: mydoc_sidebar
permalink: mydoc_factor_description.html
folder: mydoc
---



__因子库`factor_library`提供包括交易摩擦因子（市值因子、波动率因子、高阶距因子、流动性因子、Beta因子）、动量因子、价值因子、成长因子、盈利因子与财务流动性因子等六大类因子对应公司特征数据，本部分将针对每类因子的文献来源、构建方法与涵盖范围进行详细描述。__

### 市值因子

1. 总市值（market cap, mc)

   个股总市值，即个股的发行总股数与最近交易日收盘价的乘积。

   参考文献：Banz, Rolf W., 1981, The relationship between return and market value of common stocks,  Journal of Financial Economics 9, 3-18.

2. 流通市值（circulation market cap, circ_mc)

   个股流通市值，即个股的流通股数量与最近交易日收盘价的乘积。

   参考文献：Banz, Rolf W., 1981, The relationship between return and market value of common stocks,  Journal of Financial Economics 9, 3-18.

3. 非线性市值（nonlinear market cap, mc_nonlinear）

   市值的立方对市值作进行回归，得到的残差值进行标准化处理即为非线性市值因子。

   参考文献：Orr, D.J., Mashtaler, I., & Nagy, A (2012). The Barra China Equity Model (CNE5). MSCI BARRA.

4. 流通市值占总市值比重（circulation market cap to market cap ratio, circ_to_total_mc_ratio)

   个股流通市值除以总市值。

### 波动率因子

1. 1个月总波动率（one_month total volatility, vol_1m）

   过去一月的总波动率计算方式为过去20个交易日内的个股日收益率的标准差，其中标记不满10个交易日数据的股票数据为缺失值。

   参考文献：Ang, Andrew, Robert J. Hodrick, Yuhang Xing, and Xiaoyan Zhang, 2010, The Cross-Section  of Volatility and Expected Returns, Journal of Finance 61, 259-299.

2. 1个月特质波动率（one-month idosyncratic volatility，ido_vol_1m）

   过去20个交易日内的个股日收益率对市场投资组合收益率进行回归，所得残差的标准差即为特定波动率，其中标记不满10个交易日数据的股票数据为缺失值。市场投资组合收益率为A股所有股票按流通市值为权重构造的股票组合的收益率。

   参考文献：Ang, Andrew, Robert J. Hodrick, Yuhang Xing, and Xiaoyan Zhang, 2010, The Cross-Section  of Volatility and Expected Returns, Journal of Finance 61, 259-299.

3. 12个月总波动率（twelve_month total volatility, vol_1y）

   过去250个交易日内的个股日收益率的标准差，其中标记不满120个交易日数据的股票数据为缺失值。

   参考文献：Ang, Andrew, Robert J. Hodrick, Yuhang Xing, and Xiaoyan Zhang, 2010, The Cross-Section  of Volatility and Expected Returns, Journal of Finance 61, 259-299.

4. 12个月特质波动率（twelve-month idosyncratic volatility，ido_vol_1y）

   过去250个交易日内的个股日收益率对市场投资组合收益率进行回归，所得残差的标准差即为特定波动率，其中标记不满120个交易日数据的股票数据为缺失值。市场投资组合收益率为A股所有股票按流通市值为权重构造的股票组合的收益率。

   参考文献：Ang, Andrew, Robert J. Hodrick, Yuhang Xing, and Xiaoyan Zhang, 2010, The Cross-Section  of Volatility and Expected Returns, Journal of Finance 61, 259-299.

5. 总偏态（total skewness，skew）

   过去250个交易日内的股票日收益率的偏态，其中标记不满120个交易日数据的股票数据为缺失值。

   参考文献：Amaya, Diego, Peter Christoffersen, Kris Jacobs, and Aurelio Vasquez, 2015, Does realized  skewness predict the cross-section of equity returns? Journal of Financial Economics 118, 135-167.

6. 特质偏态（idiosyncratic skewness，ido_skew）

   过去250个交易日内的股票日收益率与市场投资组合日收益率进行回归，所得残差的偏态即为特质偏态，其中标记不满120个交易日数据的股票数据为缺失值。市场投资组合收益率为A股所有股票按流通市值为权重构造的股票组合的收益率。

   参考文献：Boyer, Brian, and Todd Mitton, and Keith Vorkink, 2010, Expected Idiosyncratic Skewness,  Review of Financial Studies 23, 169-202.

7. 条件偏态（conditional skewness，con_skew）

   过去250个交易日的股票日收益率与市场投资组合日收益率的平方进行回归，所得斜率系数即为共同偏态，其中标记不满120个交易日数据的股票数据为缺失值。市场投资组合超额收益率为A股所有股票按流通市值为权重构造的股票组合的收益率。

   参考文献：Harvey, Campbell R., and Akhtar Siddique, 1999, Autoregressive Conditional Skewness,  Journal of Financial & Quantitative Analysis 34, 465-487.

8. 最大日收益率（maxiumn daily return，ret_max）

   过去20个交易日的股票日收益率的最大值，其中标记不满10个交易日数据的股票数据为缺失值。

   参考文献：Bali, Turan G., and Nusret Cakici, and Robert F. Whitelaw, 2008, Maxing out: Stocks as lotteries  and the cross-section of expected returns, Journal of Financial Economics 99, 427-446.

### 流动性因子

1. 1个月交易换手率（one_month turnover，turn_1m）

   过去20个交易日内的日换手率的平均值，其中换手率计算方式为日交易量除以流通股数，并标记不满10个交易日数据的股票数据为缺失值。

   参考文献：Datar, Vinay T., and Narayan Y. Naik, and Robert Radcliffe, 1998, Liquidity and stock returns:  An alternative test, Journal of Financial Markets 1, 203-219.

2. 1个月交易换手率波动率（volatility of one_month turnover, turn_std_1m）

   过去20个交易日内的日换手率的标准差，其中换手率计算方式为日交易量除以流通股数，并标记不满10个交易日数据的股票数据为缺失值。

   参考文献：Tarun Chordia, Avanidhar Subrahmanyam, and V. Ravi Anshuman, 2001, Trading activity and  expected stock returns, Journal of Financial Economics 3, 32.

3. 12个月交易换手率（twelve_month turnover, turn_1y）

   过去250个交易日内的日换手率的平均值，其中换手率计算方式为日交易量除以流通股数，并标记不满120个交易日数据的股票数据为缺失值。

   参考文献：Datar, Vinay T., and Narayan Y. Naik, and Robert Radcliffe, 1998, Liquidity and stock returns:  An alternative test, Journal of Financial Markets 1, 203-219.

4. 12个月交易换手率波动率（volatility of one_month turnover, turn_std_1y）

   过去250个交易日内的日换手率的标准差，其中换手率计算方式为日交易量除以流通股数，并标记不满120个交易日数据的股票数据为缺失值。

   参考文献：Tarun Chordia, Avanidhar Subrahmanyam, and V. Ravi Anshuman, 2001, Trading activity and  expected stock returns, Journal of Financial Economics 3, 32.

5. 异常换手率（abnormal turnover，turn_abn）

   过去20个交易日的日换手率的平均值与过去252个交易日的日换手率的平均值的比值，其中标记过去20个交易日内不满10个交易日数据或过去252个交易日内不满120个交易日数据的股票数据为缺失值。

   参考文献：张峥,刘力.换手率与股票收益:流动性溢价还是投机性泡沫?[J].经济学(季刊),2006(02):871-892.

6. 1个月非流动性风险（illiquidity, illiq_1m）

   过去20个交易日的日收益率绝对值除以日成交金额的平均值，其中标记不满10个交易日数据的股票数据为缺失值。

   参考文献：Amihud, Yakov, 2002, Illiquidity and Stock Returns Cross-Section and Time-Series Effects,  Journal of Financial Markets 5, 31-56.

### Beta因子

1. 市场Beta（market beta, beta）

   过去250个交易日的个股日超额收益率与市场投资组合的日超额收益率进行回归，得到的斜率系数即为股票的市场Beta，其中标记不满120个交易日数据的股票数据为缺失值。市场投资组合超额收益率为A股所有股票按流通市值为权重构造的股票组合的收益率。

   参考文献：Frazzini A, Pedersen L H. Betting against beta[J]. Journal of Financial Economics, 2014, 111(1): 1-25.

2. 下行Beta（downside beta, beta_down）

   过去250个交易日内市场投资组合的日收益率小于其日收益率平均值的条件下，个股日超额收益率与市场投资组合的日超额收益率进行回归，得到的斜率系数即为股票的下行Beta，其中标记不满120个交易日数据的股票数据为缺失值。市场投资组合超额收益率为A股所有股票按流通市值为权重构造的股票组合的收益率。
   
   参考文献：Ang, A., Chen, J., & Xing, Y. (2006). Downside risk. The review of financial studies, 19(4), 1191-1239.
   
3. 上行Beta（upside beta, beta_up）

   过去250个交易日内市场投资组合的日收益率大于于其日收益率平均值的条件下，个股日超额收益率与市场投资组合的日超额收益率进行回归，得到的斜率系数即为股票的上行Beta，其中标记不满120个交易日数据的股票数据为缺失值。市场投资组合超额收益率为A股所有股票按流通市值为权重构造的股票组合的收益率。

   参考文献：Ang, A., Chen, J., & Xing, Y. (2006). Downside risk. The review of financial studies, 19(4), 1191-1239.

4. 相对Beta（relative beta, beta_relative）

   过去250个交易日内股票上行Beta与下行Beta的差值，其中标记不满120个交易日数据的股票数据为缺失值。

5. Dimson Beta（Dimson Beta，beta_dimson）

### 动量反转因子

1. 12个月动量（12-month momentum，mom_12m）

   t日的12个月动量等于t-250交易日至t-20交易日的累计收益率，其中标记不满110个交易日数据的股票数据为缺失值。

   参考文献：Jegadeesh, Narasimhan, 1990, Evidence of Predictable Behavior of Security Returns, Journal of  Finance 45, 881-898

2. 6个月动量（6-month momtum, mom_6m）

   t日的6个月动量等于t-125交易日至t-20交易日之间的累计收益率，其中标记不满50个交易日数据的股票数据为缺失值。

   参考文献： Jegadeesh, Narasimhan, and Sheridan Titman, 1993, Returns to Buying Winners and Selling  Losers: Implications for Stock Market Efficiency, Journal of Finance 48, 65-91.

3. 1个月动量/短期反转（short_term reversal，mom_1m）

   过去20个交易日的累计收益率，其中标记不满10个交易日数据的股票数据为缺失值。

   参考文献： Jegadeesh, Narasimhan, and Sheridan Titman, 1993, Returns to Buying Winners and Selling  Losers: Implications for Stock Market Efficiency, Journal of Finance 48, 65-91.

4. 异质动量（idiosyncratic momentum，ido_mom）

   t日的异质动量构建方法为t-250交易日至t-20交易日之间的股票日收益率与市场投资组合日收益率进行回归，所得残差的和即为异质动量，其中标记不满50个交易日数据的股票数据为缺失值。

   参考文献：Blitz, David, and Joop Huij, and Martin Martens, 2011, Residual Momentum, Journal of  Empirical Finance 18, 506-521.

5. 动量变化（momentum change，mom_chg）

   t日的动量变化为t-125交易日至t-20交易日之间的动量减去t-250交易日至t-125交易日的动量，其中对t-125交易日至t-20交易日之间不满足50个交易日数据与t-250交易日至t-125交易日之间不满60个交易日数据的股票数据为缺失值。

   参考文献：Gettleman, Eric, and Joseph M. Marks, 2006, Acceleration Strategies, Working Paper.

### 价值因子

1. 账面市值比（book-to-market ratio，bm）

   账面价值除以流通市值，其中账面价值等于最新财务报表披露的股东权益合计（不包含少数股东权益）减去优先股权益，流通市值等于个股的流通股数与最新收盘价的乘积。

   参考文献：Rosenberg, Barr, and Kenneth Reid, and Ronald Lanstein, 1985, Persuasive evidence of market  inefficiency, Journal of Portfolio Management 11, 9-16.

2. 总资产市值比（asset-to-market ratio, am）

   总资产合计除以流通市值，其中总资产等于最新财务报表披露的总资产，流通市值等于个股的流通股数与最新收盘价的乘积。

   参考文献：Bhandari, Laxmi Chand, 1988, Debt/Equity Ratio and Expected Common Stock Returns:  Empirical Evidence, Journal of Finance 43, 507-528.

3. 总负债市值比（liabilities-to-market ratio，lm）

   总负债除以流通市值，其中总负债等于最新财务报表披露的总负债，流通市值等于个股的流通股数与最新收盘价的乘积。

   参考文献：Bhandari, Laxmi Chand, 1988, Debt/Equity Ratio and Expected Common Stock Returns:  Empirical Evidence, Journal of Finance 43, 507-528.

4. 收益价格比（earnings-to-price ratio，ep）

   净利润除以流通市值，其中净利润等于滚动12个月净利润（不含少数股东损益），流通市值等于个股的流通股数与最新收盘价的乘积。

   参考文献：Basu, S., 1977, Investment Performance of Common Stocks In Relation To Their Price‐ Earnings Ratios: A Test Of The Efficient Market Hypothesis, Journal of Finance 32, 20.

5. 现金流价格比（cash-flow-to-price ratio，cfp）

   净现金流除以流通市值，其中净现金流等于滚动12个月的现金及现金等价物净增加额，流通市值等于个股的流通股数与最新收盘价的乘积。

   参考文献：Lakonishok, Josef, and Andrei Shleifer, and Robert W. Vishny, 1994, Contrarian Investment,  Extrapolation, and Risk, Journal of Finance 49, 1541-1578.

6. 营业现金流价格比（operating cash-flow-to-price，ocfp）

   营业现金流除以流通市值，其中营业现金流等于滚动12个月的经营活动产生的现金流量净额，流通市值等于个股的流通股数与最新收盘价的乘积。

   参考文献：Desai, Hemang, and Shivaram Rajgopal, and Mohan Venkatachalam, 2004, Value-Glamour  and Accruals Mispricing: One Anomaly or Two? Accounting Review 79, 355-385.

7. （待修改）股利价格比（dividend-to-price ratio，dp）

   应付股利除以流通市值，其中应付股利等于滚动12个月的应付股利，流通市值等于个股的流通股数与最新收盘价的乘积。

   参考文献：Litzenberger, Robert H., and Krishna Ramaswamy, 1982, The Effects of Dividends on  Common Stock Prices: Tax Effects or Information Effects? Discussion, Journal of Finance 37, 429- 443.

8. 营业收入价格比（sales-to-price ratio，sp）

   营业收入除以流通市值，其中营业收入等于滚动12个月的营业收入，流通市值等于个股的流通股数与最新收盘价的乘积。

   参考文献：Jr, Barbee William C., and MukherjiSandip, and A. Rainesgary, 1996, Do Sales–Price and  Debt–Equity Explain Stock Returns Better than Book–Market and Firm Size? Financial Analysis Journal 52, 56-60.

### 成长因子

1. 总资产增长率（asset growth, asset_g）

   最新财务报表披露的总资产减去上一年同比总资产再除以上一年同比总资产。

   参考文献：Cooper, Michael J., and Huseyin Gulen, and Michael J. Schill, 2008, Asset Growth and the  Cross-Section of Stock Returns, Journal of Finance 63, 1609-1651.

2. 负债增长率（liabilities growth，liab_g）

   最新财务报表披露的总负债减去上一年同比总负债再除以上一年同比总负债。

   参考文献：Soliman, M. T., 2005, Accrual reliability, earnings persistence and stock prices ☆, Journal of  Accounting & Economics 39, 437-485.

3. 净资产增长率（book market value growth，bm_g）

   最新财务报表披露的股东权益合计(不含少数股东权益)减去上一年同比股东权益合计（不含少数股东权益）再除以上一年同比股东权益合计（不含少数股东权益）。

   参考文献：Soliman, M. T., 2005, Accrual reliability, earnings persistence and stock prices ☆, Journal of  Accounting & Economics 39, 437-485.

4. 营业收入（TTM）增长率（trailing 12 months sales growh，sales_g_ttm）

   最近12个月营业收入减去上一年同比营业收入再除以上一年同比营业收入。

   参考文献：Lakonishok, Josef, and Andrei Shleifer, and Robert W. Vishny, 1994, Contrarian Investment,  Extrapolation, and Risk, Journal of Finance 49, 1541-1578.

5. 营业收入（季度）增长率（quarterly sales growth, sales_g_q）

   最新财务报表披露的营业收入减去上一年同比营业收入再除以上一年同比营业收入。

   参考文献：同上。

6. 营业利润（TTM）增长率（trailing 12 months gross margin growth，gm_g_ttm）

   营业利润（TTM）增长率减去营业收入（TTM）增长率，其中营业利润（TTM）增长率等于最近12个月营业利润减去上一年同比营业利润再除以上一年同比营业利润，最近12个月营业收入减去上一年同比营业收入再除以上一年同比营业收入。

   参考文献：Bushee, B., and J. S. Abarbanell, 1997, Abnormal Returns to a Fundamental Analysis Strategy,  The Accouting Review 73, 19-45.

7. 营业利润（季度）增长率（quarterly gross margin growth, gm_g_q）

   营业利润（季度）增长率减去营业收入（季度）增长率，其中营业利润（季度）增长率等于最新披露财务报表的营业利润减去上一年同比营业利润再除以上一年同比营业利润，营业收入（季度）增长率等于最新财务报表披露的营业收入减去上一年同比营业收入再除以上一年营业收入。

   参考文献：同上。

8. 净利润（TTM）增长率（trailing 12 months profit growth, profit_g_ttm）

   最近12个月净利润（不含少数股东损益）减去上一年同比净利润（不含少数股东损益）再除以上一年同比净利润（不含少数股东损益）。

9. 净利润（季度）增长率（quarterly profit growth, profit_g_q）

   最新财务报表披露的净利润（不含少数股东损益）减去上一年同比净利润（不含少数股东损益）再除以上一年同比净利润（不含少数股东损益）。

10. 存货增长率（inventory growth，inv_g）

    最新财务报表披露的净存货额减去上一年同比净存货额再除以上一年同比净存货额。

    参考文献：Thomas, Jacob K., and Huai Zhang, 2002, Inventory Changes and Future Returns, Review of  Accounting Studies 7, 163-187.

11. 营业收入与存货增长率的差（sales growth minus inventory growth, sales_g_minus_inv_g）

    营业收入（季度）增长率减去存货增长率，其中营业收入（季度）增长率等于最近12个月净利润（不含少数股东损益）减去上一年同比营业收入（不含少数股东损益）再除以上一年同比营业收入（不含少数股东损益），存货增长率等于最新财务报表披露的净存货额减去上一年同比净存货额再除以上一年同比净存货额。 

    参考文献：Bushee, B., and J. S. Abarbanell, 1997, Abnormal Returns to a Fundamental Analysis Strategy,  The Accouting Review 73, 19-45.

12. 税收（TTM）增长率（trailing 12 months tax growth, income_tax_g_ttm）

    最近12个月所得税减去上一年同比所得税再除以上一年同比所得税。

    参考文献：Thomas, Jacob K., and Huai Zhang, 2002, Inventory Changes and Future Returns, Review of Accounting Studies 7, 163-187. 

13. 税收（季度）增长率（quarterly tax growth, income_tax_g）

    最新财务报表披露的所得税减去上一年同比所得税再除以上一年同比所得税。

    参考文献：同上。

14. 增值因子（accruals component, acc）

    增值除以平均资产合计，其中增值等于除去现金及现金等价物变化的流动资产变化减去除去债务变化和应税收入变化的流动负债再减去折旧和摊销，平均资产合计等于最新财报披露总资产与其上一年同比总资产的平均值。债务等于最新财报披露的一年内到期的非流动资产与应付票据的和，现金及现金等价物变化等于过去12个月的现金流及现金等价物净增加额，折旧和摊销等于过去12个月的固定资产折旧、油气资产折旧、生产性生物资产折旧与无形资产摊销的和。

    参考文献：Sloan, Richard G., 1996, Do Stock Prices Fully Reflect Information in Accruals and Cash Flows about Future Earnings? The Accounting Review 71, 289-315. 

15. 增值因子的绝对值（absolute accruals, acc_abs）

    增值因子的绝对值，其中增值因子的计算方式同上。

    参考文献：Bandyopadhyay, Sati P., and Alan Guoming Huang, and Tony Wirjanto, 2010, The Accrual Volatility Anomaly, Working Paper. 

16. 股东权益变化率（% change in shareholders' equity, eq_g）

    最近财务报表披露的股东权益合计（不包括少数股东权益）减去上一年同比股东权益合计（不包括少数股东权益）再除以上一年同比股东权益合计（不包括少数股东权益）

    参考文献：Richardson, Scott A., Richard G. Sloan, Mark T. Soliman, and A. Irem Tuna, 2005, Accrual Reliability, Earnings Persistence and Stock Prices, Journal of Accounting and Economics. 

17. 净经营资产（net operating assets, noa）

    净经营资产的计算方式为最新财报披露的经营资产减去经营负债再除以上一年同比的总资产，其中经营资产等于总资产减去货币资金与交易性金融资产，经营负债等于总负债减去短期借款、长期借款、少数股东权益与股东权益合计（不含少数股东权益）。

    参考文献：Hirshleifer, David, Kewei Hou, Siew Hong Teoh, and Yinglei Zhang, 2004, Do investors overvalue firms with bloated balance sheets? , Journal of Accounting & Economics 38, 297-331. 
    
18. 营业收入变化率减去存货净额变化率（% change in sales - % change in inventory, sales_g_minus_inv_g）

    营业收入（TTM）变化率减去存货净额变化率，其中营业收入（TTM）变化率等于最近12个月的营业收入减去上一年同比的营业收入除以上一年同比的营业收入，存货净额变化率等于最新财务报表披露的存货净额减去上一年同比的存货净额除以上一年同比的存货净额。

    参考文献：Bushee, B., and J. S. Abarbanell, 1997, Abnormal Returns to a Fundamental Analysis Strategy,  The Accouting Review 73, 19-45.

19. 营业收入变化率减去应收账款变化率（% change in sales - % change in accounts receivable, sales_g_minus_ar_g）

    营业收入（TTM）变化率减去应收账款变化率，其中营业收入（TTM）变化率等于最近12个月的营业收入减去上一年同比的营业收入除以上一年同比的营业收入，应收账款变化率等于最新财务报表披露的应收账款减去上一年同比的应收账款除以上一年同比的应收账款。

    参考文献：Bushee, B., and J. S. Abarbanell, 1997, Abnormal Returns to a Fundamental Analysis Strategy,  The Accouting Review 73, 19-45.

20. 营业收入变化率减去三费变化率（% change in sales - % change in SG&A, sales_g_minus_sga_g）

    营业收入（TTM）变化率减去销售、管理、财务费用总和的变化率，其中营业收入（TTM）变化率等于最近12个月的营业收入减去上一年同比的营业收入除以上一年同比的营业收入，三费变化率等于最近12个月销售、管理、财务费用总和减去上一年同比三费费用除以上一年同比三费费用。

    参考文献：Bushee, B., and J. S. Abarbanell, 1997, Abnormal Returns to a Fundamental Analysis Strategy,  The Accouting Review 73, 19-45.

21. 研发支出（research and development，rd）

    最近12个月的研发支出。

    参考文献：Guo, Re Jin, and Baruch Lev, and Charles Shi, 2006, Explaining the Short- and Long-Term  IPO Anomalies by R&D, Journal of Business Finance & Accounting 33, 580–586.

22. 研发支出市值比（R&D to market capitalization, rd_to_mc）

    最近12个月的研发支出除以最新流通市值。

    参考文献：Guo, Re Jin, and Baruch Lev, and Charles Shi, 2006, Explaining the Short- and Long-Term  IPO Anomalies by R&D, Journal of Business Finance & Accounting 33, 580–586.

### 盈利因子

1. 净资产收益（季度）率（quarterly return on equity, roe_q）

   最新财务报表披露的季度净利润(不含少数股东损益)除以最新财务报表披露的股东权益合计(不含少数股东权益)。

   参考文献：Hou, Kewei, and Chen Xue, and Lu Zhang, 2015, Digesting anomalies: An investment  approach, Review of Financial Studies 28, 650–705. 

2. 净资产收益（TTM）率（trailing twelve month return on equity, roe_ttm）

   最近12月的净利润(不含少数股东损益)除以最新财务报表披露的股东权益合计(不含少数股东权益)。

   参考文献：Hou, Kewei, and Chen Xue, and Lu Zhang, 2015, Digesting anomalies: An investment  approach, Review of Financial Studies 28, 650–705. 

3. 总资产收益（季度）率（quarterly return on assets, roa_q）

   最新财务报表披露的季度净利润(不含少数股东损益)除以最新财务报表披露的总资产。

   参考文献：Balakrishnan, Karthik, and Eli Bartov, and Lucile Faurel, 2010, Post loss/profit announcement  drift, Journal of Accounting and Economics 50, 20-41.

4. 总资产收益（TTM）率（trailing twelve month return on assets, roa_q）

   最近12月的净利润(不含少数股东损益)除以最新财务报表披露的总资产。

   参考文献：Balakrishnan, Karthik, and Eli Bartov, and Lucile Faurel, 2010, Post loss/profit announcement  drift, Journal of Accounting and Economics 50, 20-41.

5. 销售毛利（季度）率（quarterly gross profit margin, gp_q）

   最新财务报表披露的季度营业收入减去营业成本再除以营业成本。

6. 销售毛利（TTM）率（trailing twelve month gross profit magin, gp_ttm）

   最近12个月的营业收入减去营业成本再除以营业成本。

7. 资本换手率（capital turnover, ct）

   最近12月的销售收入除以平均总资产，其中平均总资产等于最新财务报表披露的总资产与上一年同比总资产的平均值。

   参考文献：Baker, N. L., 2004, Commonality in the Determinants of Expected Stock Returns, Journal of  Financial Economics 41, 401-439.

8. 利润资产比率（gross profit-to-assets, pa）

   最近12月的营业利润除以平均总资产，其中营业利润等于营业收入减去营业成本，平均总资产等于最新财务报表披露的总资产与上一年同比总资产的平均值。

   参考文献：Novy-Marx, Robert, 2013, The other side of value: The gross profitability premium ,  Journal of Financial Economics 108, 1-28.

9. 营业利润率（operating profit rate，op）

   最近12月的营业收入加其他业务收入减去销售成本、财务费用-销售费用、管理费用，再除以最新财务报表披露的股东权益总计（不包含少数股东权益）。

   参考文献：Fama, Eugene F., and Kenneth R. French, 2015, A five-factor asset pricing model Journal of  Financial Economics 116, 1-22.

10. 投入（季度）资本回报率（quarterly return on invested capital, roic_q）

    最新财务报表披露的息前税后营业利润除以投入资本，其中息前税后营业利润等于净利润加财务费用，投入资本等于资产总计减流动负债加上应付票据、短期借款与一年内到期的非流动负债。

    参考文献： Brown, David P., and Bradford Rowe, 2007, The Productivity Premium in Equity Returns,  Working Paper.

11. 投入（TTM）资本回报率（trailing twelve month return on invested capital, roic_ttm）

    最近12月的息前税后营业利润除以最新财务报表披露的投入资本，其中息前税后营业利润等于净利润加财务费用，投入资本等于资产总计减流动负债加上应付票据、短期借款与一年内到期的非流动负债。

    参考文献： Brown, David P., and Bradford Rowe, 2007, The Productivity Premium in Equity Returns,  Working Paper.

### 财务流动性因子

1. 流动比率（current ratio, cr）

   最新财务报表披露的流动资产除以流动负债。

   参考文献： Ou, Jane A., and Stephen H. Penman, 1989, Financial statement analysis and the prediction of  stock returns, Journal of Accounting & Economics 11, 295-329.

2. 速动比率（quick ratio, qr）

   流动资产减去净存货额再除以流动负债。

   参考文献： Ou, Jane A., and Stephen H. Penman, 1989, Financial statement analysis and the prediction of  stock returns, Journal of Accounting & Economics 11, 295-329.

3. 现金流负债比率（cash flow to debt ratio, cf_to_debt）

   最新财务报表披露的季度经营现金净流量除以流动负债。

   参考文献： Ou, Jane A., and Stephen H. Penman, 1989, Financial statement analysis and the prediction of  stock returns, Journal of Accounting & Economics 11, 295-329.

4. 营业收入现金比（sales to cash ratio, sales_to_cash）

   最新财务报表披露的季度营业收入除以货币资金。

   参考文献： Ou, Jane A., and Stephen H. Penman, 1989, Financial statement analysis and the prediction of  stock returns, Journal of Accounting & Economics 11, 295-329.

5. 营业收入存货比（sales to inventory ratio, sales_to_inv）

   最新财务报表披露的季度营业收入除以存货净额。

   参考文献： Ou, Jane A., and Stephen H. Penman, 1989, Financial statement analysis and the prediction of  stock returns, Journal of Accounting & Economics 11, 295-329.

6. 流动比率增长率（current ratio growth，cr_g）

   最新财务报表披露的流动比率（流动资产除以流动负债）减去上一年同比流动比率再除以上一年同比流动比率。

   参考文献： Ou, Jane A., and Stephen H. Penman, 1989, Financial statement analysis and the prediction of  stock returns, Journal of Accounting & Economics 11, 295-329.

7. 速动比率增长率（quick ratio growh, qr_g）

   最新财务报表披露的速动比率（流动资产减去净存货额的差除以流动负债）减去上一年同比速动比率再除以上一年同比速动比率。

   参考文献： Ou, Jane A., and Stephen H. Penman, 1989, Financial statement analysis and the prediction of  stock returns, Journal of Accounting & Economics 11, 295-329.

8. 营业收入存货比增长率（% change sales-to-inventory, sales_to_inv_g）

   最新财务报表披露的营业收入存货比（季度营业收入除以存货净额）减去上一年同比营业收入存货比再除以上一年同比营业搜狐如存货比。

   参考文献： Ou, Jane A., and Stephen H. Penman, 1989, Financial statement analysis and the prediction of  stock returns, Journal of Accounting & Economics 11, 295-329.

9. 营业收入应收账款比（sales to receivable, sales_to_receiv）

   最新财务报表披露的季度营业收入除以应收账款。

   参考文献： Ou, Jane A., and Stephen H. Penman, 1989, Financial statement analysis and the prediction of  stock returns, Journal of Accounting & Economics 11, 295-329.

10. 偿债能力/总资产（firm tangibility, tang）

    最新财务报表披露的货币资金加0.715倍应收账款、0.547倍存货净值与0.535倍固定资产的和，再除以总资产合计。

    参考文献： Almeida, Heitor, and Murillo Campello, 2007, Financial Constraints, Asset Tangibility, and  Corporate Investment, Review of Financial Studies, 20, 1429-1460.
