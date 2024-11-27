### 用途说明

save_to_database 函数用于将数据保存到指定的 SQLite 数据库文件中。

### 参数

* data (DataFrame):  需要保存到数据库的 Pandas DataFrame 数据。
* db_path (str): 数据库文件的路径。
* table_name (str):  数据库中要创建或替换的表的名称。
### 用法

调用 save_to_database(data, db_path, table_name) 函数，将 data 中的数据保存到 db_path 指定的数据库文件中的 table_name 表中。如果表已经存在，则会替换现有表。

### 示例

```python
import sqlite3
import pandas as pd
import yuhanbolh as lh

# 示例数据
data = pd.DataFrame({'name': ['Alice', 'Bob'], 'age': [25, 30]})

# 数据库文件路径
db_path = 'my_database.db'

# 表名
table_name = 'users'

# 保存数据到数据库
lh.save_to_database(data, db_path, table_name)
```

### 流程图

```mermaid
graph TD
    A[开始] --> B{准备数据: data, db_path, table_name}
    B --> C{建立数据库连接}
    C --> D{创建/替换表}
    D --> E{写入数据}
    E --> F{关闭连接}
    F --> G[结束]
    C -- 连接失败 --> H[打印错误信息]
    H --> G
```

