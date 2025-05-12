## 用途说明

计算动量震荡指标(AO)，并根据AO的形态生成交易信号。

## 参数

* data (DataFrame): 包含股票或交易品种历史数据的DataFrame，至少包含'high'和'low'两列。
## 返回值

* DataFrame: 包含AO交易信号的DataFrame，列名为'AO'，其中：
## 用法

函数调用示例及返回值说明。

## 示例

```python
import pandas as pd

# 假设data是包含'high'和'low'列的DataFrame
# data = pd.DataFrame({'high': [..., ...], 'low': [..., ...]})
# 调用AO_zb函数
signals = AO_zb(data)

# 打印信号
print(signals)
```

## 函数工作流程图

```mermaid
graph TD
    A[开始] --> B{计算5日和34日均价};
    B --> C{计算AO值};
    C --> D{判断茶碟形买入信号};
    D -- 是 --> E[生成买入信号 (1)];
    D -- 否 --> F{判断向上穿过零线信号};
    F -- 是 --> E;
    F -- 否 --> G{判断茶碟形卖出信号};
    G -- 是 --> H[生成卖出信号 (-1)];
    G -- 否 --> I{判断向下穿过零线信号};
    I -- 是 --> H;
    I -- 否 --> J[生成中立信号 (0)];
    E --> K[输出信号];
    H --> K;
    J --> K;
    K --> L[结束];
```

## 函数代码

```python
import numpy as np
import pandas as pd

# 计算动量震荡指标(AO)，参数只有一个，即数据源
def AO_zb(data):
    # 计算Awesome Oscillator（AO）
    AO = (data['high'].rolling(5).mean() + data['low'].rolling(5).mean()) / 2 - (data['high'].rolling(34).mean() + data['low'].rolling(34).mean()) / 2

    # 定义茶碟形买入的条件
    AO_plus_saucer = (AO.shift(2) < AO.shift(1)) & (AO.shift(1) < AO) & (AO > 0)
    # 定义向上穿过零线的条件
    AO_plus_cross = (AO.shift(1) < 0) & (AO > 0)

    # 定义茶碟形卖出的条件
    AO_minus_saucer = (AO.shift(2) > AO.shift(1)) & (AO.shift(1) > AO) & (AO < 0)
    # 定义向下穿过零线的条件
    AO_minus_cross = (AO.shift(1) > 0) & (AO < 0)

    # 根据条件计算买入、卖出和中立的信号
    signal = np.where(AO_plus_saucer | AO_plus_cross, 1, np.where(AO_minus_saucer | AO_minus_cross, -1, 0))

    # 返回包含所有历史数据的DataFrame
    return pd.DataFrame({'AO': signal
    })
```

