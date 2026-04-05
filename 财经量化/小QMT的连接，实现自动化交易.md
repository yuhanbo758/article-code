---
创建时间: 2024-01-18 20:57
修改时间: 2024-01-18 21:05
tags:
  - 量化交易
  - python
  - qmt
share: "true"
---

[小QMT的连接，实现自动化交易_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1AN4y1W7uj/)
#### 一、程序功能概述

本文介绍的是一段自动化股票交易程序的代码，它能够实现在指定时间内自动连接股票交易平台，执行交易操作，并持续监控账户状态。程序利用了多线程技术，确保交易任务的持续运行和监控，并且能够在遇到异常时自动重连，保证交易的连续性和稳定性。

### 二、代码

```python
global schedule_thread
schedule_thread = None

# 运行交易程序，参数有4个：交易端路径、资金账号、数据库路径、计划任务函数
# 例如：run_stock_trading_bot(r'D:\国金证券QMT交易端\userdata_mini', '885451429', r'D:\wenjian\python\smart\data\guojin_account.db', schedule_jobs)
def run_stock_trading_bot(path, account_id, db_path, schedule_jobs):
    global schedule_thread  # 使用 global 声明以引用全局变量

    while True:
        try:
            current_time = time.strftime("%H:%M", time.localtime())
            if "08:30" <= current_time <= "21:20":
                session_id = int(random.randint(100000, 999999))
                xt_trader = XtQuantTrader(path, session_id)
                acc = StockAccount(account_id)
                callback = MyXtQuantTraderCallback()
                xt_trader.register_callback(callback)
                xt_trader.start()

                connect_result = xt_trader.connect()
                if connect_result != 0:
                    print('连接失败，程序即将重试')
                else:
                    subscribe_result = xt_trader.subscribe(acc)
                    if subscribe_result != 0:
                        print('账号订阅失败 %d' % subscribe_result)

                    asset = xt_trader.query_stock_asset(acc)
                    if asset:
                        save_stock_asset(asset, db_path)
                        print("证券资产查询保存成功,可用资金：", asset.cash)

                    # 检查计划任务线程是否活跃，如果不活跃则启动
                    if schedule_thread is None or not schedule_thread.is_alive():
                        schedule_thread = threading.Thread(target=schedule_jobs)
                        schedule_thread.start()

                    while xt_trader:
                        time.sleep(10)
                        current_time = datetime.now().strftime("%H:%M")
                        if current_time > "21:20":
                            break
                    print("连接断开，即将重新连接")
            else:
                print("当前时间不在运行时段内")
                time.sleep(3600)  # 睡眠一小时后再次检查
        except Exception as e:
            print(f"运行过程中发生错误: {e}")
            time.sleep(3600)  # 如果遇到异常，休息一小时再试
```
#### 三、代码结构解析

1. **全局变量定义**：`schedule_thread`用于存储计划任务线程，以保证在程序运行过程中，定时任务能够正确执行。
    
2. **主函数定义**：`run_stock_trading_bot`是主要的交易函数，包含四个参数：交易端路径、资金账号、数据库路径和计划任务函数。
    
3. **无限循环**：程序使用了一个无限循环，确保在交易时间内持续运行。
    
4. **时间判断**：通过判断当前时间是否在交易时间内（08:30至21:30），来决定是否执行交易程序。
    
5. **交易端连接与账户订阅**：首先初始化交易端对象，然后尝试连接交易端。若连接失败，则程序将在输出错误信息后重试。连接成功后，程序会订阅资金账号以获取交易信息。
    
6. **资产查询与保存**：查询股票资产信息，并将信息保存到指定的数据库中。
    
7. **计划任务线程的检查与启动**：检查计划任务线程是否活跃，若不活跃则启动线程，以确保定时任务可以按计划执行。
    
8. **异常处理与重连机制**：程序包含异常处理机制，当发生错误时，程序会在记录错误信息后休息一小时再尝试重连。
    

#### 四、程序的实际应用

这段代码在股票交易自动化领域具有重要意义。它能够减少人工干预，提高交易效率，并且通过实时监控和自动重连机制，增加了交易过程的稳定性和可靠性。特别适合量化交易者和那些希望实现交易自动化的投资者。

#### 五、技术点分析

1. **多线程应用**：通过多线程技术，程序能够同时执行交易任务和监控任务，提高了程序的效率和响应速度。
    
2. **时间管理**：程序根据时间判断是否执行交易操作，这一点对于遵守交易时间规则非常重要。
    
3. **异常处理**：程序中的异常处理机制能够确保程序在遇到问题时不会直接崩溃，而是尝试解决问题后继续运行。
    

#### 六、总结

该程序是一个高效、稳定的股票交易自动化工具，适用于各种量化交易策略。它不仅提高了交易效率，也为投资者提供了更稳定可靠的交易体验。

