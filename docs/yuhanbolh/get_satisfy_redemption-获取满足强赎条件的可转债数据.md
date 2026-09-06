# get_satisfy_redemption：获取满足强赎条件的可转债数据

获取强赎条件查询的六列数据；查询失败抛出 WencaiError。

## 调用签名

```python
get_satisfy_redemption(query)
```

## 参数

| 参数 | 默认值 | 说明 |
| --- | --- | --- |
| query | 必填 | 自然语言筛选语句，不能为空。 |## 返回结果

固定列：可转债代码、可转债简称、最新价、正股代码、正股简称、强赎天计数。

## 配置和异常

调用前配置环境变量 IWENCAI_API_KEY，可选 IWENCAI_BASE_URL。无需网页Cookie或Node.js。参数错误抛出ValueError，查询失败抛出WencaiError（RuntimeError子类）；失败不等于成功无候选。完整分页失败不会返回部分数据。可选指标未返回时为缺失值，调用者应检查策略必需指标。

## 最小示例

```python
import yuhanbolh as lh

result = lh.get_satisfy_redemption("可转债；满足强赎；强赎天计数")
print(result)
```

## 本次更新

2026-09-06：配合OpenAPI、AKShare 1.18.94和标准桥接集成更新。本文为本地文档，需用户自行同步远端。

