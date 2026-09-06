## 用途说明

该函数用于从指定的SQLite数据库文件中读取指定数据表的所有数据。

## 参数

* db_path (str): 数据库文件的路径。
* table_name (str): 要读取数据的数据表的名称。
## 用法

调用 get_existing_data(db_path, table_name) 函数，传入数据库文件路径和数据表名称，函数将返回一个包含所有数据的 Pandas DataFrame。如果读取数据时发生错误，函数将打印错误信息并返回一个空的 DataFrame。

## 示例

```python
import sqlite3
import pandas as pd
import yuhanbolh as lh

db_file = "mydatabase.db"
table = "customers"

data = lh.get_existing_data(db_file, table)

if not data.empty:
  print("数据库数据：")
  print(data)
else:
  print("无法读取数据库数据。")
```

## 流程图

```mermaid
graph TD
    A[开始] --> B{数据库连接成功？}
    B -- 是 --> C[执行SQL查询]
    C --> D[将查询结果转换为DataFrame]
    D --> E[返回DataFrame]
    B -- 否 --> F[打印错误信息]
    F --> G[返回空的DataFrame]
    E --> H[结束]
    G --> H
```

