---
创建时间: 2024-01-16 09:11
修改时间: 2024-01-16 09:15
tags:
  - python量化
  - python
  - 量化分析
share: "true"
---



下面代码使用 `pytdx` 库从通达信获取金融数据。`pytdx` 是一个用于获取中国股市数据的 Python 库，它通过连接到通达信的服务器来获取股票交易数据。这个示例脚本展示了如何使用 `pytdx` 库从通达信服务器获取分笔成交数据。

```python
from pytdx.hq import TdxHq_API

# 直接输入 hqget 即可进入交互模式，进入之后，先选择要连接的服务器类型，然后选择要执行的功能，选择菜单里面最后一项退出交互模式。
# https://gitee.com/better319/pytdx/

def get_financial_data(server_ip, server_port, data_function):
    try:
        api = TdxHq_API()

        if api.connect(server_ip, server_port):
            data = data_function(api)  # 使用传入的函数获取数据
            if data is None:
                api.disconnect()
                return "No data received."

            df = api.to_df(data)  # 转换为DataFrame
            api.disconnect()
            return df
        else:
            return "Connection failed."
    except Exception as e:
        return f"An exception occurred: {str(e)}"

# 获取通达信的分笔成交数据，参数：服务器IP、服务器端口、函数
df = get_financial_data('119.147.212.81', 7709, lambda api: api.get_transaction_data(0, '000001', 0, 30))
print(df)
```
### 代码解释

1. **引入库**：
   ```python
   from pytdx.hq import TdxHq_API
   ```
   这行代码导入了 `pytdx` 库中的 `TdxHq_API` 类，用于与通达信的服务器建立连接并获取数据。

2. **定义函数 `get_financial_data`**：
   这个函数用于连接通达信服务器，获取金融数据，并将其转换为 `pandas.DataFrame` 格式。
   - **参数**：
     - `server_ip`：服务器的 IP 地址。
     - `server_port`：服务器的端口号。
     - `data_function`：一个函数，当与服务器连接成功后，此函数被调用以获取数据。
   - **异常处理**：
     使用 `try...except` 块来处理可能出现的异常，如连接失败或数据获取错误。

3. **连接服务器并获取数据**：
   使用 `api.connect()` 方法尝试连接到服务器。如果连接成功，调用传入的 `data_function` 函数来获取数据，然后使用 `api.to_df()` 方法将数据转换为 `pandas.DataFrame`。如果数据获取失败或连接失败，函数返回相应的错误信息。

4. **使用示例**：
   ```python
   df = get_financial_data('119.147.212.81', 7709, lambda api: api.get_transaction_data(0, '000001', 0, 30))
   ```
   这行代码示例了如何使用 `get_financial_data` 函数获取股票代码为 '000001' 的前 30 条分笔成交数据。

### 作用

这段代码的主要作用是方便用户从通达信获取股票市场的实时数据，特别是分笔成交数据。这对于进行股市分析和决策非常有用，因为它提供了市场动态的深入视角。

# 交互模式
该库提供交互模式，直接输入 hqget 即可进入交互模式，进入之后，先选择要连接的服务器类型，然后选择要执行的功能，选择菜单里面最后一项退出交互模式。