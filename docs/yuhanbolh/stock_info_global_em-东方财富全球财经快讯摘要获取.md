## 用途说明

获取东方财富全球财经快讯，共200条，并只保留摘要信息。

## 参数

无

## 返回值

pandas.DataFrame: 包含财经快讯摘要的数据框，列名为“摘要”。

## 用法

函数调用示例及返回值说明。

## 示例

```python
import pandas as pd
from 获取东财快讯200 import stock_info_global_em

# 调用函数获取财经快讯摘要
df = stock_info_global_em()

# 打印结果
print(df)
```

## 函数工作流程图

```mermaid
graph TD
    A[开始] --> B{发起 HTTP 请求};
    B --> C{解析 JSON 数据};
    C --> D{创建 DataFrame};
    D --> E{选取 "summary" 列};
    E --> F{重命名列为 "摘要"};
    F --> G[返回 DataFrame];
    G --> H[结束]
```

## 函数代码

```python
import requests
import pandas as pd

# 获取东方财富全球财经快讯，共200条，只保留摘要
def stock_info_global_em() -> pd.DataFrame:
    """
    东方财富-全球财经快讯
    https://kuaixun.eastmoney.com/7_24.html
    :return: 全球财经快讯摘要
    :rtype: pandas.DataFrame
    """
    url = "https://np-weblist.eastmoney.com/comm/web/getFastNewsList"
    params = {
        "client": "web",
        "biz": "web_724",
        "fastColumn": "102",
        "sortEnd": "",
        "pageSize": "200",
        "req_trace": "1710315450384",
    }
    r = requests.get(url, params=params)
    data_json = r.json()
    temp_df = pd.DataFrame(data_json["data"]["fastNewsList"])
    temp_df = temp_df[["summary"]]
    temp_df.rename(
        columns={
            "summary": "摘要",
        },
        inplace=True,
    )
    return temp_df
```

