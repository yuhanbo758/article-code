# akshare_convertible_bond：获取集思录可转债强赎数据

返回 AKShare 集思录可转债强赎原始表；网络异常向调用方传播。

## 调用签名

```python
akshare_convertible_bond()
```

## 参数

无参数。

## 返回结果

AKShare原始18列DataFrame，包括强赎状态、强赎天计数。数据源：集思录。

## 异常与数据边界

网络、缺列、重复页或分页不完整均抛出异常，不把部分结果当成完整数据。成功空表仍保留约定列。数据日期由上游决定，周末返回缓存不代表实时交易日行情。

## 最小示例

```python
import yuhanbolh as lh

result = lh.akshare_convertible_bond()
print(result)
```

## 本次更新

2026-09-06：配合OpenAPI、AKShare 1.18.94和标准桥接集成更新。本文为本地文档，需用户自行同步远端。

