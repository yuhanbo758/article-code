## 用途说明

该函数用于获取指定股票代码列表的实时行情数据，并根据条件筛选出符合要求的标的，返回包含筛选结果的数据表。

## 参数

* code_list (List[str]): 股票代码列表，例如：['000001.SZ', '600000.SH']。
## 返回值

* df (pd.DataFrame): 包含筛选结果的数据表，列名如下：
## 用法

调用 get_snapshot(code_list) 函数，传入股票代码列表，即可获取筛选后的行情数据。

## 示例

```python
import pandas as pd
from typing import List
import yuhanbolh as lh

# ... (假设 xtdata 库已安装并导入)

code_list = ['000001.SZ', '600000.SH']
df = lh.get_snapshot(code_list)
print(df)
```

## 函数流程图

```mermaid
graph TD
    A[开始] --> B{获取股票代码列表<br> `code_list`}
    B --> C{调用 `xtdata.get_full_tick(code_list)`<br> 获取实时行情数据}
    C --> D{数据预处理<br> (计算均价、格式转换)}
    D --> E{筛选数据<br> (现价大于1的标的)}
    E --> F{计算衍生指标<br> (涨跌幅等)}
    F --> G{返回数据表 `df`}
    G --> H[结束]
```

