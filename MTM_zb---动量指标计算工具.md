## 用途说明

计算并判断金融品种的动量指标，生成相应的交易信号。

## 参数

* data (DataFrame): 包含金融时间序列数据的DataFrame，至少包含'close'列。
## 用法

根据动量指标的变化，生成买入、卖出或中立信号。

## 示例

```python
import pandas as pd
import numpy as np

# 示例数据
data = pd.DataFrame({'close': [10, 11, 12, 11, 13, 14, 15, 14, 13, 14, 15, 16, 15]})
mtm_signals = MTM_zb(data)
print(mtm_signals)
```

## 函数流程图

```mermaid
graph TD
    A[开始] --> B{计算MTM};
    B --> C{MTM值上升?};
    C -- 是 --> D[生成买入信号(1)];
    C -- 否 --> E{MTM值下跌?};
    E -- 是 --> F[生成卖出信号(-1)];
    E -- 否 --> G[生成中立信号(0)];
    D --> H[返回信号];
    F --> H;
    G --> H;
    H --> I[结束];
```

## 函数代码

```python
# 计算动量指标(10)，参数只有一个，即数据源
def MTM_zb(data):
    # 计算MTM值：当前收盘价与10天前的收盘价之差
    MTM = data['close'] - data['close'].shift(10)
    
    # 根据MTM值的变化确定信号
    # MTM值上升时，信号为1（买入）
    # MTM值下跌时，信号为-1（卖出）
    # MTM值无变化时，信号为0（中立）
    signal = np.where(MTM > MTM.shift(1), 1, np.where(MTM < MTM.shift(1), -1, 0))
    
    # 返回包含所有历史数据的DataFrame
    return pd.DataFrame({'MTM': signal})
```

