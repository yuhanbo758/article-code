## 用途说明

计算指定数据的线性回归，返回预期值和残差标准差。

## 参数

* data (DataFrame): 包含时间序列数据的 Pandas DataFrame，其中必须包含名为 'close' 的列。
* years_list (list): 包含需要计算线性回归的年份的列表。例如，[1, 2, 3]。
## 用法

函数调用示例及返回值说明。

返回值:
返回一个包含预期值和残差标准差的 DataFrame。

## 示例

```python
import pandas as pd
import numpy as np

# 假设 data 是包含 'close' 列的 DataFrame
data = pd.DataFrame({'close': np.random.rand(100)})
years_list = [1, 2]
result = linear_regression_dfcf_zb(data, years_list)
print(result)
```

## 函数流程图

```mermaid
graph TD
    A[开始] --> B{循环 years_list 中的每一年 many_years};
    B --> C{计算 percent：percent = round(len(data) / 7 * many_years)};
    C --> D{提取最近 percent 个数据点的 'close' 值到 y};
    D --> E{创建 x：x = np.arange(len(y))};
    E --> F{进行线性回归：slope, intercept, r_value, p_value, std_err = stats.linregress(x, y)};
    F --> G{计算预期值：expected_value = intercept + slope * len(y)};
    G --> H{计算残差：residuals = y - (intercept + slope * x)};
    H --> I{计算残差标准差：std_residuals = np.std(residuals)};
    I --> J{创建包含 expected_value 和 std_residuals 的 DataFrame};
    J --> K{将 DataFrame 添加到 df_list};
    K --> L{many_years 循环结束？};
    L -- 是 --> M{合并 df_list 中的所有 DataFrame 到 result};
    L -- 否 --> B;
    M --> N[返回 result];
```

## 函数代码

```python
import pandas as pd
import numpy as np
from scipy import stats

# 计算线性回归
def linear_regression_dfcf_zb(data, years_list):
    df_list = []
    for many_years in years_list:
        percent = round(len(data) / 7 * many_years) # 计算用于回归的数据百分比
        y = data.iloc[-percent:]['close'].values # 使用 'close' 列，提取数据
        x = np.arange(len(y)) # 创建 x 值数组
        slope, intercept, r_value, p_value, std_err = stats.linregress(x, y) # 执行线性回归
        expected_value = intercept + slope * len(y) # 计算预期值
        residuals = y - (intercept + slope * x) # 计算残差
        std_residuals = np.std(residuals) # 计算残差的标准差

        columns = [f"expected_value_{many_years}year", f"std_residuals_{many_years}year"] # 创建列名
        result_data = [expected_value, std_residuals] # 创建数据
        result_df = pd.DataFrame(data=[result_data], columns=columns) # 创建 DataFrame

        df_list.append(result_df) # 将 DataFrame 添加到列表
    result = pd.concat(df_list, axis=1) # 合并所有 DataFrame

    return result # 返回结果
```

