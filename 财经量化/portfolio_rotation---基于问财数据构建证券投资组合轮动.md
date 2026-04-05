### 用途说明

该函数根据委托备注信息，利用问财平台获取对应证券数据，并结合委托数量和策略名称，构建用于投资组合轮动的DataFrame数据结构。

### 参数

* order_note (str): 委托备注信息，包含要查询的证券信息，例如 "招商银行"、"平安银行"、"伊利股份" 等。
* order_quantity (int): 委托数量，表示对应证券的交易数量。
* strategy_name (str): 策略名称，用于标识该笔交易所属的投资策略。
### 返回值

* pandas.DataFrame: 包含以下列的DataFrame数据结构：
### 用法

通过传入委托备注、委托数量和策略名称，调用 portfolio_rotation(order_note, order_quantity, strategy_name) 函数，即可获取构建好的DataFrame数据，用于后续的投资组合轮动分析。

### 示例

```python
import pywencai
import yuhanbolh as lh

securities_data = lh.portfolio_rotation(order_note='招商银行 平安银行', order_quantity=1000, strategy_name='银行股轮动')
print(securities_data)
```

### 函数工作流程图

```mermaid
graph TD
    A[开始] --> B{判断委托备注类型};
    B -- 基金 --> C[设置查询类型为'fund'];
    B -- 转债 --> D[设置查询类型为'conbond'];
    B -- 其他 --> E[设置查询类型为'stock'];
    C --> F{调用 pywencai.get() 获取数据};
    D --> F;
    E --> F;
    F --> G{提取证券代码列并重命名};
    G --> H{添加委托备注、委托数量、策略名称列};
    H --> I[返回DataFrame数据];
    I --> J[结束];
```

```python
# 问财根据委托备注获取数据
def portfolio_rotation(order_note, order_quantity, strategy_name):
    try:
        if '基金' in order_note:
            query_type = 'fund'
        elif '转债' in order_note:
            query_type = 'conbond'
        else:
            query_type = 'stock'

        data = pywencai.get(query=order_note, query_type=query_type, loop=True)
        
        # 提取第一列数据并重命名为"证券代码"
        securities_codes = data.iloc[:, 0].rename('证券代码').to_frame()
        
        # 增加多列数据
        securities_codes = securities_codes.assign(
            委托备注=order_note,
            委托数量=order_quantity,
            策略名称=strategy_name
        )

        return securities_codes
    
    except Exception as e:
        # 捕获所有异常并打印错误信息
        print(f"发生异常: {e}")
        return None  # 返回 None 或其他适当的值以表示失败
```

