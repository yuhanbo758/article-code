# get_clean_data：问财可转债数据清洗函数

获取并清洗可转债十二列数据，保留满足强赎及强赎天计数。

## 调用签名

```python
get_clean_data(question)
```

## 参数

| 参数 | 默认值 | 说明 |
| --- | --- | --- |
| question | 必填 | 自然语言查询语句，不能为空。 |## 返回结果

固定12列：可转债代码、可转债简称、涨跌幅、最新价、正股代码、正股简称、纯债价值、期权价值、最新变动后余额、转股溢价率、满足强赎、强赎天计数。

## 配置和异常

调用前配置环境变量 IWENCAI_API_KEY，可选 IWENCAI_BASE_URL。无需网页Cookie或Node.js。参数错误抛出ValueError，查询失败抛出WencaiError（RuntimeError子类）；失败不等于成功无候选。完整分页失败不会返回部分数据。可选指标未返回时为缺失值，调用者应检查策略必需指标。

## 最小示例

```python
import yuhanbolh as lh

result = lh.get_clean_data("可转债；涨跌幅；满足强赎；强赎天计数")
print(result)
```

## 本次更新

2026-09-06：配合OpenAPI、AKShare 1.18.94和标准桥接集成更新。本文为本地文档，需用户自行同步远端。

