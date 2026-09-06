# wencai_conditional_query：问财可转债策略数据爬取工具

获取可转债策略十列数据，余额单位亿元；无匹配返回固定列空表。

## 调用签名

```python
wencai_conditional_query(query, fetch_all=True, page_size=100, timeout=60)
```

## 参数

| 参数 | 默认值 | 说明 |
| --- | --- | --- |
| query | 必填 | 自然语言筛选语句，不能为空。 |
| fetch_all | True | True获取全部分页，False仅第一页。 |
| page_size | 100 | 每页条数，正整数，默认100。 |
| timeout | 60 | 问财为单次HTTP超时秒数；桥接构造超时须大于60秒，events为服务端长轮询等待秒数。 |## 返回结果

固定列：可转债代码、可转债简称、最新价、正股代码、正股简称、纯债价值、期权价值、最新变动后余额、转股溢价率、转股价值。余额为亿元、溢价率为百分数。

## 配置和异常

调用前配置环境变量 IWENCAI_API_KEY，可选 IWENCAI_BASE_URL。无需网页Cookie或Node.js。参数错误抛出ValueError，查询失败抛出WencaiError（RuntimeError子类）；失败不等于成功无候选。完整分页失败不会返回部分数据。可选指标未返回时为缺失值，调用者应检查策略必需指标。

## 最小示例

```python
import yuhanbolh as lh

result = lh.wencai_conditional_query("可转债；债券余额；纯债价值；转股溢价率")
print(result)
```

## 本次更新

2026-09-06：配合OpenAPI、AKShare 1.18.94和标准桥接集成更新。本文为本地文档，需用户自行同步远端。

