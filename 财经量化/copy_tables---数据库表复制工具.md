## 用途说明

copy_tables 函数用于将一个 SQLite 数据库中的多个数据表复制到另一个 SQLite 数据库中。

## 参数

* table_names (list): 需要复制的表名列表，例如：['table1', 'table2', 'table3']。
## 用法

调用 copy_tables(table_names) 函数，传入需要复制的表名列表即可。函数将自动连接到源数据库和目标数据库，并将指定的表复制到目标数据库中。

## 示例

```python
import sqlite3
import yuhanbolh as lh

# 定义需要复制的表名列表
table_names = ['users', 'products', 'orders']

# 调用 copy_tables 函数复制数据表
lh.copy_tables(table_names)

print(f"已成功复制数据表：{', '.join(table_names)}")
```

## 流程图

```mermaid
graph TD
    A[开始] --> B{连接数据库};
    B{连接数据库} --> C{获取表名列表};
    C{获取表名列表} --> D{遍历表名};
    D{遍历表名} --> E{获取表结构};
    E{获取表结构} --> F{获取表数据};
    F{获取表数据} --> G{删除目标表(如果存在)};
    G{删除目标表(如果存在)} --> H{创建目标表};
    H{创建目标表} --> I{插入数据};
    I{插入数据} --> J{提交更改};
    J{提交更改} --> K{关闭连接};
    K{关闭连接} --> L[结束];
```

