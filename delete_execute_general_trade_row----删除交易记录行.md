### 用途说明

该函数用于删除 execute_general_trade 表中指定策略名称和证券代码的交易记录行。

### 参数

* cursor (cursor object): 数据库连接游标对象。
* conn (connection object): 数据库连接对象。
* strategy (str): 要删除的交易记录对应的策略名称。
* code (str): 要删除的交易记录对应的证券代码。
### 用法

调用 delete_execute_general_trade_row(cursor, conn, strategy, code)  函数并传入数据库连接游标对象、数据库连接对象、策略名称和证券代码，即可删除 execute_general_trade 表中对应数据行。

### 示例

```python
import yuhanbolh as lh

# 建立数据库连接
conn = sqlite3.connect('my_database.db')
cursor = conn.cursor()

# 调用函数删除策略名称为 "策略A"，证券代码为 "600000" 的交易记录
lh.delete_execute_general_trade_row(cursor, conn, "策略A", "600000")

# 关闭数据库连接
conn.close()
```

### 流程图

```mermaid
graph TD
    A[开始] --> B{建立数据库连接}
    B --> C{调用函数 delete_execute_general_trade_row(cursor, conn, strategy, code)}
    C --> D{执行 SQL 删除语句}
    D --> E{提交数据库修改}
    E --> F{关闭数据库连接}
    F --> G[结束]
```

```python
# 删除execute_general_trade表中的行
def delete_execute_general_trade_row(cursor, conn, strategy, code):
    """
    删除execute_general_trade表中的行
    """
    cursor.execute("DELETE FROM execute_general_trade WHERE 策略名称=? AND 证券代码=?", (strategy, code))
    conn.commit()
```

