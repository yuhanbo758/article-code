## 用途说明

根据提供的股票或金融资产的历史数据，计算Bull Bear Power（BBP）指标，并生成相应的买卖信号。

## 参数

* data (DataFrame): 包含股票或金融资产历史数据的DataFrame，至少包含'high'（最高价）、'low'（最低价）和'close'（收盘价）列。
* n (int): 计算BBP指标的周期长度，通常设置为20，但在TradingView上常使用13。
## 返回值

DataFrame: 包含BBP买卖信号的DataFrame，其中：

* 列名为'BBP'
* 1表示买入信号
* -1表示卖出信号
* 0表示无信号
## 用法

1. 准备包含历史数据的DataFrame，确保包含'high'、'low'和'close'列。
1. 调用BBP_zb函数，传入数据和周期长度。
1. 根据返回的DataFrame中的信号进行交易决策。
## 示例

```python
import pandas as pd
import numpy as np

# 示例数据
data = pd.DataFrame({
    'high': [10, 12, 15, 14, 16, 17, 15, 14, 13, 12],
    'low': [8, 9, 11, 12, 13, 14, 12, 11, 10, 9],
    'close': [9, 11, 13, 13, 15, 16, 13, 12, 11, 10]
})

# 计算BBP指标，周期为13
bbp_signals = BBP_zb(data, 13)

# 打印信号
print(bbp_signals)
```

## 函数工作流程图

```mermaid
graph TD
    A[开始] --> B{输入数据和周期长度n};
    B --> C{计算牛市力量 (high - EMA(close, n))};
    C --> D{计算熊市力量 (low - EMA(close, n))};
    D --> E{计算BBP (牛市力量 + 熊市力量)};
    E --> F{计算n日移动平均线};
    F --> G{确定股价趋势 (高于均线为1，低于为-1，否则为0)};
    G --> H{生成买卖信号};
    H --> I[输出包含信号的DataFrame];
    I --> J[结束];
```

## 函数代码

```python
import pandas as pd
import numpy as np

def BBP_zb(data, n):
    # 计算牛市力量（BullPower）和熊市力量（BearPower）
    bullPower = data['high'] - data['close'].ewm(span=n).mean()
    bearPower = data['low'] - data['close'].ewm(span=n).mean()
    
    # 计算BBP值
    BBP = bullPower + bearPower
    
    # 计算n天的移动平均值
    moving_avg = data['close'].rolling(window=n).mean()

    # 确定股价趋势：1表示上升，-1表示下降，0表示无明显趋势
    trend = np.where(data['close'] > moving_avg, 1, 
                     np.where(data['close'] < moving_avg, -1, 0))

    
    # 根据牛市力量、熊市力量和股价趋势来决定买卖信号
    signal = np.where((trend == 1) & (bearPower < 0) & (bearPower > bearPower.shift(1)), 1, 
                      np.where((trend == -1) & (bullPower > 0) & (bullPower < bullPower.shift(1)), -1, 0))
    
    # 返回BBP值和买卖信号的DataFrame
    return pd.DataFrame({'BBP' : signal})
```

