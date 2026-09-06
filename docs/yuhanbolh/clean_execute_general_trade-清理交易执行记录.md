### 用途说明

该函数用于清理 execute_general_trade 表中的无效交易记录，确保该表只包含根据 receive_condition 表中策略和证券代码组合生成的有效交易记录。

### 参数

* conn: 数据库连接对象。
### 工作流程

```mermaid
graph TD
    A[开始] --> B{连接数据库};
    B --> C[查询 receive_condition 表];
    C --> D{获取有效策略和证券代码组合};
    D --> E[查询 execute_general_trade 表];
    E --> F{遍历交易记录};
    F --> G{判断交易记录是否有效};
    G -- 有效 --> J[提交更改];
    G -- 无效 --> H[删除无效记录];
    H --> F;
    J --> K[结束];
```

### 代码

```python
# 清洗execute_general_trade表
def clean_execute_general_trade(conn):
    """
    清洗execute_general_trade表
    """
    cursor = conn.cursor()
    # 从receive_condition获取(策略名称, 证券代码)的集合
    cursor.execute("SELECT 策略名称, 证券代码 FROM receive_condition")
    receive_keys = set(cursor.fetchall())

    # 获取execute_general_trade中非'问财轮动-注询问'的所有行
    cursor.execute("SELECT rowid, 策略名称, 证券代码 FROM execute_general_trade WHERE 策略名称 != '问财轮动-注询问'")
    rows = cursor.fetchall()
    for rowid, strategy, code in rows:
        if (strategy, code) not in receive_keys:
            cursor.execute("DELETE FROM execute_general_trade WHERE rowid=?", (rowid,))
    conn.commit()
```

