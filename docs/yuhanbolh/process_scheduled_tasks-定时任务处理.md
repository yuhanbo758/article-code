# process_scheduled_tasks：定时任务处理

处理定时任务

## 调用签名

```python
process_scheduled_tasks(scheduled_tasks, cursor, conn)
```

## 参数

| 参数 | 默认值 | 说明 |
| --- | --- | --- |
| scheduled_tasks | 必填 | (rowid, code, price, quantity, buy_sell, strategy, remark, datetime_str)组成的任务列表。 |
| cursor | 必填 | 调用者管理的SQLite游标。 |
| conn | 必填 | 调用者管理的SQLite连接；成功任务可能提交委托表修改。 |## 返回结果

返回None。查询失败或无候选跳过当前任务，不执行该任务的删除、写入或委托生成；成功且非空仍按原有策略逻辑写库。

## 配置和异常

调用前配置环境变量 IWENCAI_API_KEY，可选 IWENCAI_BASE_URL。无需网页Cookie或Node.js。参数错误抛出ValueError，查询失败抛出WencaiError（RuntimeError子类）；失败不等于成功无候选。完整分页失败不会返回部分数据。可选指标未返回时为缺失值，调用者应检查策略必需指标。

## 最小示例

```python
import sqlite3
from contextlib import closing
import yuhanbolh as lh

# 空任务示例不生成委托；实际使用须传入用户自己的任务和数据库。
with closing(sqlite3.connect(":memory:")) as conn:
    lh.process_scheduled_tasks([], conn.cursor(), conn)
```

## 本次更新

2026-09-06：配合OpenAPI、AKShare 1.18.94和标准桥接集成更新。本文为本地文档，需用户自行同步远端。

