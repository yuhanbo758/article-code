## 用途说明

计算简单移动平均线（MA）指标，并根据MA线与收盘价的关系生成交易信号。

## 参数

* data (DataFrame): 包含股票或外汇数据的DataFrame，必须包含'close'列。
* n (int): 移动平均线的周期。
## 返回值

* DataFrame: 包含交易信号的DataFrame，列名为'MA_' + str(n)，其中1表示买入信号，-1表示卖出信号，0表示无信号。
## 用法

1. 准备包含股票或外汇数据的DataFrame，确保包含'close'列。
1. 调用MA_zb函数，传入数据和周期参数。
1. 根据返回的DataFrame中的信号进行交易决策。
## 示例

```python
import pandas as pd
import numpy as np

# 示例数据
data = pd.DataFrame({
    'close': [10, 12, 15, 14, 16, 18, 17, 19, 20, 22]
})

# 计算10日移动平均线指标
ma_signal = MA_zb(data, 10)
print(ma_signal)

```

## 函数工作流程图

```mermaid
graph TD
    A[开始] --> B{获取收盘价序列};
    B --> C{计算n日移动平均线};
    C --> D{比较MA与收盘价};
    D --> E{收盘价 > MA?};
    E -- 是 --> F[生成买入信号 (1)];
    E -- 否 --> G{收盘价 < MA?};
    G -- 是 --> H[生成卖出信号 (-1)];
    G -- 否 --> I[生成无信号 (0)];
    F --> J[输出信号];
    H --> J;
    I --> J;
    J --> K[结束];
```

## 函数代码

```python
import pandas as pd
import numpy as np

# 获取指数移动平均线，参数有2个，一个是数据源，一个是日期。例如EMA_zb(data, 20)
def MA_zb(data, n):
    # 计算n日简单移动平均线
    MA = pd.Series(data['close'].rolling(n).mean(), name='MA_' + str(n))
    # 获取收盘价序列
    close = data['close']
    # 根据MA与收盘价的关系生成信号
    signal = np.where(MA < close, 1, np.where(MA > close, -1, 0))
    return pd.DataFrame(signal, columns=['MA_' + str(n)])  # 修改这行
```

