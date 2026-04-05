## 用途说明

计算商品通道指标（CCI），并根据CCI的数值和变化生成交易信号。

## 参数

* data (DataFrame): 包含交易数据的DataFrame，必须包含'high'（最高价）、'low'（最低价）和'close'（收盘价）列。
* n (int): CCI计算的周期长度。通常设置为20。
## 返回值

DataFrame: 包含交易信号的DataFrame，列名为CCI_{n}。

* 1: 买入信号
* -1: 卖出信号
* 0: 无信号
## 使用方法

1. 准备包含'high'、'low'和'close'列的DataFrame。
1. 调用CCI_zb(data, n)，传入数据和周期长度。
1. 根据返回的DataFrame中的信号进行交易决策。
## 示例

```python
import pandas as pd
import numpy as np

# 示例数据
data = pd.DataFrame({
    'high': [10, 12, 15, 14, 16, 15, 13, 12, 14, 16],
    'low': [8, 9, 11, 12, 13, 12, 10, 9, 11, 13],
    'close': [9, 11, 13, 13, 15, 14, 11, 11, 13, 15]
})

# 计算CCI指标
cci_signals = CCI_zb(data, 20) # 调用 CCI_zb 函数，设置周期为20
print(cci_signals)
```

## 流程图

```mermaid
graph TD
    A[开始] --> B{计算TP: (最高价 + 最低价 + 收盘价) / 3};
    B --> C{计算MA: TP的n日移动平均};
    C --> D{计算MD: TP的n日平均绝对偏差};
    D --> E{计算CCI: (TP - MA) / (0.015 * MD)};
    E --> F{计算前一个周期的CCI};
    F --> G{生成买入信号: CCI < -100 且 CCI > 前一个周期的CCI};
    G --> H{生成卖出信号: CCI > 100 且 CCI < 前一个周期的CCI};
    H --> I{根据信号赋值: 买入=1, 卖出=-1, 无信号=0};
    I --> J[返回包含信号的DataFrame];
    J --> K[结束];
```

## 函数代码

```python
import pandas as pd
import numpy as np

def CCI_zb(data, n):
    # 计算典型价格 (Typical Price)
    TP = (data['high'] + data['low'] + data['close']) / 3
    # 计算n日移动平均
    MA = TP.rolling(n).mean()
    # 计算平均绝对偏差
    MD = TP.rolling(n).apply(lambda x: np.abs(x - x.mean()).mean())
    # 计算CCI
    CCI = (TP - MA) / (0.015 * MD)

    # 计算前一个周期的CCI
    CCI_prev = CCI.shift(1)

    # 买入信号：CCI < -100 且 CCI > 前一个周期的CCI
    buy_signal = (CCI < -100) & (CCI > CCI_prev)
    # 卖出信号：CCI > 100 且 CCI < 前一个周期的CCI
    sell_signal = (CCI > 100) & (CCI < CCI_prev)
    # 生成信号：买入为1，卖出为-1，否则为0
    signal = np.where(buy_signal, 1, np.where(sell_signal, -1, 0))
    
    return pd.DataFrame({'CCI_' + str(n): signal})
```

