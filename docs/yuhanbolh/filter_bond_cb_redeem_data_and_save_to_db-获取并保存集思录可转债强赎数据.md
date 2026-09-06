# filter_bond_cb_redeem_data_and_save_to_db：获取并保存集思录可转债强赎数据

筛选已公告/即将强赎可转债，返回七列数据。

强赎状态与强赎天计数分别保留；可转债代码加 .SH/.SZ 后缀。
db_path 默认为 None，仅取数；显式传入时替换“满足赎回可转债”表。
网络或缺列异常会终止，不把错误当空表写入数据库。

## 调用签名

```python
filter_bond_cb_redeem_data_and_save_to_db(db_path=None)
```

## 参数

| 参数 | 默认值 | 说明 |
| --- | --- | --- |
| db_path | None | 默认None只返回DataFrame；显式传入SQLite路径才替换对应表，连接结束可靠关闭。 |## 返回结果

固定7列：可转债代码、可转债简称、最新价、正股代码、正股简称、强赎状态、强赎天计数。显式db_path时替换满足赎回可转债表。

## 异常与数据边界

网络、缺列、重复页或分页不完整均抛出异常，不把部分结果当成完整数据。成功空表仍保留约定列。数据日期由上游决定，周末返回缓存不代表实时交易日行情。

## 最小示例

```python
import yuhanbolh as lh

result = lh.filter_bond_cb_redeem_data_and_save_to_db()
print(result)
```

## 本次更新

2026-09-06：配合OpenAPI、AKShare 1.18.94和标准桥接集成更新。本文为本地文档，需用户自行同步远端。

