### 用途说明

该函数用于向数据库插入一条市价委托记录。

### 参数

* conn (object): 数据库连接对象。
* magic (int): EA 的 magic number。
* symbol (str): 交易品种。
* volume (float): 交易量。
* sl (float): 止损价。
* tp (float): 止盈价。
* deviation (int): 价格偏差。
* type (int): 订单类型。
* comment (str): 订单注释。
### 用法

调用 market_order_fn() 函数并传入相关参数，即可向数据库插入一条市价委托记录。

### 示例

```python
import yuhanbolh as lh
# 建立数据库连接
conn = sqlite3.connect('trading.db')

# 调用函数插入市价委托记录
lh.market_order_fn(conn, 12345, 'EURUSD', 0.1, 1.0500, 1.1000, 5, 0, 'Test Order')

# 关闭数据库连接
conn.close()
```

### 流程图

```mermaid
graph TD
    A[开始] --> B{建立数据库连接};
    B --> C{调用 market_order_fn（） 函数};
    C --> D{插入市价委托记录};
    D --> E{关闭数据库连接};
    E --> F[结束];
```

## 代码

```python
# 插入市价委托，参数：conn为数据库连接对象，magic为EA的magic number，symbol为交易品种，volume为交易量，sl为止损价，tp为止盈价，deviation为价格偏差，type为订单类型，comment为订单注释
def market_order_fn(conn, magic, symbol, volume, sl, tp, deviation, type, comment):
    try:
        insert_query = """
        INSERT INTO forex_order (交易类型, EA_id, 订单号, 品种名称, 交易量, 价格, Limit挂单, 止损, 止盈, 价格偏差, 订单类型, 成交类型, 订单有效期, 订单到期, 订单注释, 持仓单号, 反向持仓单号) 
        VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?)
        """

        # 插入的值
        values = (1, magic, 0, symbol, volume, 0, 0, sl, tp, deviation, type, 1, 0, 0, comment, 0, 0)

        # 执行插入操作
        conn.execute(insert_query, values)
        conn.commit()

    except Exception as e:
        print("An error occurred:", e)
```

