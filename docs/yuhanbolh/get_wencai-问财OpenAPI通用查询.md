# get_wencai：问财OpenAPI通用查询

按自然语言查询股票/基金/可转债/美股，返回原始业务字段 DataFrame。

loop=False 只取第一页。成功无匹配返回含证券代码、证券简称的空表；
配置、HTTP、协议或分页失败抛出 WencaiError，不返回部分数据。
IWENCAI_API_KEY 必填，IWENCAI_BASE_URL 可指定服务根地址或完整接口。

## 调用签名

```python
get_wencai(question, query_type='stock', loop=True, *, page_size=100, timeout=60)
```

## 参数

| 参数 | 默认值 | 说明 |
| --- | --- | --- |
| question | 必填 | 自然语言查询语句，不能为空。 |
| query_type | 'stock' | stock / fund / conbond / usstock；限定自然语言查询范围。 |
| loop | True | True获取全部分页，False仅第一页。 |
| page_size | 100 | 每页条数，正整数，默认100。 |
| timeout | 60 | 问财为单次HTTP超时秒数；桥接构造超时须大于60秒，events为服务端长轮询等待秒数。 |## 返回结果

保留服务端原始业务字段的DataFrame。成功空结果含证券代码、证券简称列。

## 配置和异常

调用前配置环境变量 IWENCAI_API_KEY，可选 IWENCAI_BASE_URL。无需网页Cookie或Node.js。参数错误抛出ValueError，查询失败抛出WencaiError（RuntimeError子类）；失败不等于成功无候选。完整分页失败不会返回部分数据。可选指标未返回时为缺失值，调用者应检查策略必需指标。

## 最小示例

```python
import yuhanbolh as lh

result = lh.get_wencai("可转债；债券余额", query_type="conbond")
print(result)
```

## 本次更新

2026-09-06：配合OpenAPI、AKShare 1.18.94和标准桥接集成更新。本文为本地文档，需用户自行同步远端。

