# portfolio_rotation：基于问财数据构建证券投资组合轮动

基于问财数据构建证券投资组合轮动

## 调用签名

```python
portfolio_rotation(order_note, order_quantity, strategy_name)
```

## 参数

| 参数 | 默认值 | 说明 |
| --- | --- | --- |
| order_note | 必填 | 问财查询语句；包含基金或ETF/转债时选择相应市场，其他为A股。 |
| order_quantity | 必填 | 输出表中的委托数量，本函数本身不下单。 |
| strategy_name | 必填 | 策略名称；桥接订单要求非空且不超过20个GBK字节。 |## 返回结果

证券代码、委托备注、委托数量、策略名称；明确按代码列名读取，不使用第一列。

## 配置和异常

调用前配置环境变量 IWENCAI_API_KEY，可选 IWENCAI_BASE_URL。无需网页Cookie或Node.js。参数错误抛出ValueError，查询失败抛出WencaiError（RuntimeError子类）；失败不等于成功无候选。完整分页失败不会返回部分数据。可选指标未返回时为缺失值，调用者应检查策略必需指标。

## 最小示例

```python
import yuhanbolh as lh

result = lh.portfolio_rotation("可转债；债券余额大于1亿元", 10, "示例策略")
print(result)
```

## 本次更新

2026-09-06：配合OpenAPI、AKShare 1.18.94和标准桥接集成更新。本文为本地文档，需用户自行同步远端。

