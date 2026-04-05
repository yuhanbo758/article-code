## 用途说明

计算股票或其他金融资产的终极震荡指标（Ultimate Oscillator，UO），并生成相应的交易信号。

## 参数

* data (DataFrame): 包含金融资产历史数据的DataFrame，必须包含'high'（最高价）、'low'（最低价）和'close'（收盘价）列。
* n1 (int): 第一个时间周期，用于计算短期平均买入压力和真实范围的比值。
* n2 (int): 第二个时间周期，用于计算中期平均买入压力和真实范围的比值。
* n3 (int): 第三个时间周期，用于计算长期平均买入压力和真实范围的比值。
## 返回值

* DataFrame: 包含交易信号的DataFrame，其中：
## 用法

1. 准备包含'high'、'low'和'close'列的DataFrame数据。
1. 调用UO_zb函数，传入数据和三个时间周期参数。
1. 根据返回的DataFrame中的信号进行交易决策。
## 示例

```python
import pandas as pd
import numpy as np

# 示例数据
data = pd.DataFrame({
    'high': [10, 12, 15, 14, 16, 18, 17],
    'low': [8, 9, 11, 12, 13, 15, 14],
    'close': [9, 11, 14, 13, 15, 17, 16]
})

# 计算UO指标并生成信号
signal_df = UO_zb(data, 7, 14, 28)
print(signal_df)
```

## 函数工作流程图

```mermaid
graph TD
    A[开始] --> B{准备数据 (high, low, close)};
    B --> C{计算最小 low 或 close};
    C --> D{计算最大 high 或 close};
    D --> E{计算买入压力 (bp)};
    E --> F{计算真实范围 (tr_)};
    F --> G{计算不同时间周期内的平均比值 (avg7, avg14, avg28)};
    G --> H{计算终极震荡指标 (UO)};
    H --> I{生成交易信号 (1, -1, 0)};
    I --> J[结束];
```

## 函数代码

```python
import pandas as pd
import numpy as np

def UO_zb(data, n1, n2, n3):
    # 计算前一天的收盘价和今天的最低价中的最小值
    min_low_or_close = pd.concat([data['low'], data['close'].shift(1)], axis=1).min(axis=1)
    
    # 计算前一天的收盘价和今天的最高价中的最大值
    max_high_or_close = pd.concat([data['high'], data['close'].shift(1)], axis=1).max(axis=1)
    
    # 计算买入压力
    bp = data['close'] - min_low_or_close
    
    # 计算真实范围
    tr_ = max_high_or_close - min_low_or_close
    
    # 计算不同时间范围内的平均买入压力和真实范围的比值
    avg7 = bp.rolling(n1).sum() / tr_.rolling(n1).sum()
    avg14 = bp.rolling(n2).sum() / tr_.rolling(n2).sum()
    avg28 = bp.rolling(n3).sum() / tr_.rolling(n3).sum()
    
    # 计算终极指标UO
    UO = 100 * ((4 * avg7) + (2 * avg14) + avg28) / 7
    
    # 生成信号
    # UO > 70，生成买入信号1
    # UO < 30，生成卖出信号-1
    # 其他情况，生成中立信号0
    signal = np.where(UO > 70, 1, np.where(UO < 30, -1, 0))
    
    return pd.DataFrame({'UO': signal})
```

