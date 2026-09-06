## 用途说明

计算成交量加权移动平均线（VWMA），并根据VWMA与收盘价的关系生成交易信号。

## 参数

* data (DataFrame): 包含股票或交易品种历史数据的DataFrame，必须包含'close'（收盘价）和'volume'（成交量）列。
* n (int): 计算VWMA的窗口期。
## 返回值

* DataFrame: 包含交易信号的DataFrame，列名为'VWMA_' + str(n)。信号值：1表示买入，-1表示卖出，0表示中性。
## 用法

1. 准备包含'close'和'volume'列的历史数据DataFrame。
1. 调用VWMA_zb函数，传入数据和窗口期参数。
1. 分析返回的DataFrame中的交易信号。
## 示例

```python
import pandas as pd
import numpy as np

# 示例数据
data = pd.DataFrame({
    'close': [10, 12, 15, 14, 16, 18, 17, 19, 20, 22],
    'volume': [100, 120, 150, 140, 160, 180, 170, 190, 200, 220]
})

# 计算10日VWMA指标
vwma_signal = VWMA_zb(data, 10)
print(vwma_signal)
```

## 函数工作流程图

```mermaid
graph TD
    A[开始] --> B{计算 VWMA};
    B --> C{收盘价 > VWMA?};
    C -- 是 --> D[生成买入信号 (1)];
    C -- 否 --> E{收盘价 < VWMA?};
    E -- 是 --> F[生成卖出信号 (-1)];
    E -- 否 --> G[生成中性信号 (0)];
    D --> H[返回信号 DataFrame];
    F --> H;
    G --> H;
    H --> I[结束];
```

## 函数代码

```python
import numpy as np
import pandas as pd

def VWMA_zb(data, n):
    # 计算VWMA
    vwma = (data['close'] * data['volume']).rolling(n).sum() / data['volume'].rolling(n).sum()
    
    # 根据VWMA和收盘价计算买卖信号
    buy_signal = vwma < data['close']
    sell_signal = vwma > data['close']
    signal = np.where(buy_signal, 1, np.where(sell_signal, -1, 0))
    
    return pd.DataFrame(signal, columns=['VWMA_' + str(n)])
```

