---
创建时间: 2024-02-19 18:45
修改时间: 2024-02-19 21:00
tags:
  - python
  - 股票
  - 量化分析
标题: 用 Python 打造你的股市分析工具箱：从数据获取到 K 线图绘制
share: "true"
---


[用 Python 打造你的股市分析工具箱：从数据获取到 K 线图绘制_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1bH4y1E7dM/?vd_source=247ac77d4ae7339ea06d0fec09aa8f70)

K 线图是金融市场中常用的技术分析工具，可以直观地展示股票价格的走势和波动情况。本文将介绍如何使用 Python 和 akshare、mplfinance 库来获取东方财富网的股票日线数据并绘制 K 线图。

### 代码

```python
import akshare as ak
import mplfinance as mpf
import pandas as pd
import matplotlib.pyplot as plt

# 设置 Matplotlib 支持中文显示
plt.rcParams['font.sans-serif'] = ['Microsoft YaHei'] # 设置中文字体，确保中文能够正常显示
plt.rcParams['axes.unicode_minus'] = False # 解决负号 '-' 显示为方块的问题

def get_stock_data_eastmoney(symbol, start_date, end_date):
  # 使用 akshare 的 stock_zh_a_hist 函数获取东方财富网的股票日线数据
  df = ak.stock_zh_a_hist(symbol=symbol, period="daily", start_date=start_date, end_date=end_date, adjust="qfq")

  # 检查获取的 DataFrame 是否为空
  if df.empty:
    print("未获取到数据，请检查股票代码及日期范围是否正确。")
    return

  # 将日期列设置为索引，并转换为 datetime 类型
  df['日期'] = pd.to_datetime(df['日期'])
  df.set_index('日期', inplace=True)

  # 调整 DataFrame 列名以符合 mplfinance 的要求
  df.rename(columns={
    '开盘': 'Open',
    '收盘': 'Close',
    '最高': 'High',
    '最低': 'Low',
    '成交量': 'Volume'
  }, inplace=True)

  # 转换列名为小写，以符合 mplfinance 的要求
  df.columns = df.columns.str.lower()

  # 定义 mplfinance 的自定义风格
  mc = mpf.make_marketcolors(up='r', down='g', volume='inherit')
  s = mpf.make_mpf_style(base_mpf_style='charles', marketcolors=mc, rc={'font.sans-serif': ['Microsoft YaHei']})

  # 使用 mplfinance 绘制 K 线图，并应用自定义风格
  mpf.plot(df, type='candle', style=s,
       title=f"{symbol} K 线图",
       ylabel='价格',
       ylabel_lower='成交量',
       volume=True,
       mav=(5,20,60),
       show_nontrading=False)

# 调用函数，获取股票数据并绘制 K 线图
get_stock_data_eastmoney('600519', '20200101', '20201231') # 示例股票代码和日期范围
```

如
### 代码说明

1. 首先，导入所需的库：
    
    - `akshare`: 用于获取东方财富网的股票数据
    - `mplfinance`: 用于绘制 K 线图
    - `pandas`: 用于数据处理
    - `matplotlib`: 用于图形显示
2. 然后，定义函数 `get_stock_data_eastmoney`，用于获取指定股票代码和日期范围的股票日线数据。
    
3. 在函数中，首先使用 `akshare.stock_zh_a_hist` 函数获取数据。
    
4. 接着，检查获取的数据是否为空。
    
5. 然后，将日期列设置为索引，并转换为 `datetime` 类型。
    
6. 之后，调整 DataFrame 列名以符合 `mplfinance` 的要求。
    
7. 接下来，定义 `mplfinance` 的自定义风格。
    
8. 最后，使用 `mplfinance.plot` 函数绘制 K 线图，并应用自定义风格。
    
9. 最后，调用函数，获取示例股票代码和日期范围的 K 线图。

#### 数据获取与处理

`akshare`是一个开源财经数据接口库，它提供了获取各种财经数据的API，包括股票、期货、基金等。本文中，我们使用`akshare`的`stock_zh_a_hist`函数，从东方财富网抓取指定股票的历史日线数据。这个函数需要输入股票代码、数据周期（日线）、起始日期和结束日期。通过调整“qfq”参数，我们可以获取到前复权的数据，这对于长期分析尤为重要，因为它考虑了股票分红和拆分的影响。

获取到的数据是一个`DataFrame`，我们通过`pandas`库对其进行处理。首先，将日期列设置为索引并转换为`datetime`类型，这对后续的时间序列分析至关重要。接下来，我们将列名调整为`mplfinance`库能够识别的格式（小写的'open'、'close'、'high'、'low'、'volume'），以便进行K线图的绘制。

#### 数据可视化

`mplfinance`是一个专门用于财经数据可视化的库，它提供了绘制K线图、成交量图和移动平均线等功能。在本文中，我们利用`mplfinance`绘制了包含K线、成交量和移动平均线（5天、20天、60天）的图表。为了使图表更加直观和美观，我们通过`mpf.make_marketcolors`和`mpf.make_mpf_style`自定义了图表的风格和颜色，其中红色代表上涨，绿色代表下跌。

为了支持中文显示并解决一些常见的显示问题（如负号'-'显示为方块），我们还对`matplotlib`的全局配置进行了调整，设置了中文字体和解决了负号显示问题。

#### 结论

通过上述步骤，我们不仅获取了指定股票的历史数据，还将其以直观的形式展现了出来。这对于分析股票的历史表现、识别市场趋势和做出投资决策具有重要意义。Python 和其相关库的强大功能，使得这一切变得既简单又高效。



