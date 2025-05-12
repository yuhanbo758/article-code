### 用途说明

计算威廉百分比变动（Williams %R），并生成买卖信号。

### 参数

* data (DataFrame): 包含股票或金融资产历史数据的DataFrame，必须包含'high'、'low'和'close'列。
* n (int): 计算WPR的周期长度，通常为14。
### 返回值

DataFrame: 包含买卖信号的DataFrame，其中：

* 1表示买入信号。
* -1表示卖出信号。
* 0表示中立信号。
### 使用方法

1. 准备包含'high'、'low'和'close'列的DataFrame数据。
1. 调用WPR_zb函数，传入数据和周期长度。
1. 根据返回的DataFrame中的信号进行交易决策。
### 示例

```python
import pandas as pd
import numpy as np

# 示例数据
data = pd.DataFrame({
    'high': [100, 102, 105, 103, 106],
    'low': [95, 97, 98, 99, 100],
    'close': [98, 100, 102, 101, 104]
})

# 计算WPR指标
signal_df = WPR_zb(data, 3)

# 打印结果
print(signal_df)
```

### 流程图

```mermaid
graph TD
    A[开始] --> B{准备数据};
    B --> C{计算WPR};
    C --> D{判断WPR是否超买超卖};
    D -- 是 --> E{生成买卖信号};
    D -- 否 --> F{信号为0};
    E --> G[结束];
    F --> G;
```

### 函数代码

```python
def WPR_zb(data, n):
    # 计算WPR（Williams %R）值
    WPR = pd.Series((data['high'].rolling(n).max() - data['close']) / 
                    (data['high'].rolling(n).max() - data['low'].rolling(n).min()) * -100, 
                    name='WPR_' + str(n))
    
    # 设置上下轨
    lower_band = -80
    upper_band = -20
    
    # 根据WPR值和上下轨确定买卖信号
    # 当WPR < 下轨且正在上升时，信号为1（买入）
    # 当WPR > 上轨且正在下跌时，信号为-1（卖出）
    # 否则，信号为0（中立）
    signal = np.where((WPR < lower_band) & (WPR > WPR.shift(1)), 1, 
                      np.where((WPR > upper_band) & (WPR < WPR.shift(1)), -1, 0))

    # 返回包含所有历史数据的DataFrame
    return pd.DataFrame({'WPR_' + str(n):  signal})
```

