## 用途说明

根据MACD指标的金叉和死叉生成交易信号。

## 参数

* data (DataFrame): 包含交易数据的DataFrame，必须包含'close'列。
* n_fast (int):  快速EMA的周期，通常设置为12。
* n_slow (int):  慢速EMA的周期，通常设置为26。
## 返回值

DataFrame: 包含交易信号的DataFrame，'MACD'列为信号值：

* 1：金叉信号（买入）。
* -1：死叉信号（卖出）。
* 0：无信号（中性）。
## 用法

```python
import pandas as pd
# 示例数据
data = pd.DataFrame({
    'close': [10, 11, 12, 11, 10, 12, 13, 14, 13, 12]
})

# 调用MACD_Level_zb函数计算MACD信号
macd_signal_df = MACD_Level_zb(data, 12, 26)

# 打印结果
print(macd_signal_df)
```

## 流程图

```mermaid
graph TD
    A[开始] --> B{计算快速EMA};
    B --> C{计算慢速EMA};
    C --> D{计算MACD (快EMA - 慢EMA)};
    D --> E{计算MACD信号线};
    E --> F{判断MACD与信号线};
    F -- MACD > 信号线 --> G[输出买入信号 (1)];
    F -- MACD < 信号线 --> H[输出卖出信号 (-1)];
    F -- MACD == 信号线 --> I[输出中性信号 (0)];
    G --> J[结束];
    H --> J;
    I --> J;
```

## 函数代码

```python
def MACD_Level_zb(data, n_fast, n_slow):
     # 计算快速EMA
    EMAfast = data['close'].ewm(span=n_fast, min_periods=n_slow).mean()
    
    # 计算慢速EMA
    EMAslow = data['close'].ewm(span=n_slow, min_periods=n_slow).mean()
    
    # 计算MACD值，即快速EMA与慢速EMA之差
    MACD = EMAfast - EMAslow
    
    # 计算MACD的信号线值
    MACDsignal = MACD.ewm(span=9, min_periods=9).mean()
    
    # 根据MACD和其信号线值确定信号
    # 主线值 > 信号线值时，信号为1（买入）
    # 主线值 < 信号线值时，信号为-1（卖出）
    # 主线值等于信号线值时，信号为0（中立）
    signal = np.where(MACD > MACDsignal, 1, np.where(MACD < MACDsignal, -1, 0))
    
    # 返回包含所有历史数据的DataFrame
    return pd.DataFrame({'MACD': signal})
```

