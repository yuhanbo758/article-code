## 用途说明

计算Hull MA（船体移动平均线）指标，并根据HullMA和收盘价生成买卖信号。

## 参数

* data (DataFrame): 包含股票或金融资产历史数据的DataFrame，必须包含'close'列。
* n (int, 可选): Hull MA的周期长度，默认为9。
## 返回值

* DataFrame: 包含买卖信号的DataFrame，列名为'HullMA_' + str(n)，其中：
## 用法

1. 准备包含'close'列的DataFrame数据。
1. 调用HullMA_zb函数，传入数据和周期长度n。
1. 分析返回的DataFrame，根据信号值进行交易决策。
## 示例

```python
import pandas as pd
import numpy as np
import math

# 示例数据
data = pd.DataFrame({
    'close': [10, 11, 12, 13, 12, 14, 15, 14, 16, 17]
})

# 计算Hull MA并生成信号
hullma_signals = HullMA_zb(data, n=9)
print(hullma_signals)
```

## 函数工作流程图

```mermaid
graph TD
    A[开始] --> B{输入数据和周期n};
    B --> C{计算WMA1: WMA(收盘价, n // 2) * 2};
    C --> D{计算WMA2: WMA(收盘价, n)};
    D --> E{计算HullMA: WMA(WMA1 - WMA2, sqrt(n))};
    E --> F{比较HullMA和收盘价};
    F -- HullMA < 收盘价 --> G[生成买入信号 (1)];
    F -- HullMA > 收盘价 --> H[生成卖出信号 (-1)];
    F -- 其他 --> I[无信号 (0)];
    G --> J[输出信号DataFrame];
    H --> J;
    I --> J;
    J --> K[结束];
```

```python
import numpy as np
import pandas as pd
import math

def HullMA_zb(data, n=9):
    def wma(series, period):
        weights = np.arange(1, period + 1)
        return series.rolling(period).apply(lambda x: np.dot(x, weights) / weights.sum(), raw=True)
    
    source = data['close']
    wma1 = wma(source, n // 2) * 2
    wma2 = wma(source, n)
    hullma = wma(wma1 - wma2, int(math.floor(math.sqrt(n))))

    # 根据HullMA和收盘价计算买卖信号
    buy_signal = hullma < source
    sell_signal = hullma > source
    signal = np.where(buy_signal, 1, np.where(sell_signal, -1, 0))
    
    return pd.DataFrame(signal, columns=['HullMA_' + str(n)])
```

