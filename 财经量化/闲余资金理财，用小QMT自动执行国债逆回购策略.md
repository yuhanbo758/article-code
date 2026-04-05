---
创建时间: 2024-01-19 17:15
修改时间: 2024-01-19 19:42
tags:
  - 量化交易
  - python
  - qmt
share: "true"
---

[闲余资金理财，用小QMT自动执行国债逆回购策略_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1xK4y1B7dz/)
# 国债逆回购策略代码

这段代码的主要目的是自动化进行沪深两市一天期国债逆回购的交易，在收盘之前，或下午 4 点钟之前，自动进行国债逆回购，用闲余资金理财获取收益
```python
# 比较沪深两市的一天期的买一国债逆回购，选择值大的进行卖出
def place_order_based_on_asset(xt_trader, acc, xtdata):
    # 检查连接结果
    connect_result = xt_trader.connect()
    if connect_result == 0:
        print('连接成功')
        try:
            # 查询证券资产
            asset = xt_trader.query_stock_asset(acc)
            print("证券资产查询保存成功, 可用资金：", asset.cash)

            # 判断可用资金是否足够
            if asset.cash >= 1000:
                # 根据资产计算订单量
                order_volume = int(asset.cash / 1000) * 10

                # 获取市场数据以确定股票代码和价格
                xtdata.subscribe_quote('131810.SZ', period='tick', start_time='', end_time='', count=1, callback=None)
                xtdata.subscribe_quote('204001.SH', period='tick', start_time='', end_time='', count=1, callback=None)
                generate_func = xtdata.get_market_data(field_list=['bidPrice'], stock_list=['131810.SZ','204001.SH'], period='tick', start_time='', end_time='', count=-1, dividend_type='none', fill_data=True)

                # 提取 '131810.SZ' 和 '204001.SH' 的最后一个 bidPrice
                price_131810 = generate_func['131810.SZ']['bidPrice'][-1][0]
                price_204001 = generate_func['204001.SH']['bidPrice'][-1][0]

                # 根据价格选择股票代码和价格
                if price_131810 >= price_204001:
                    stock_code, price = '131810.SZ', price_131810
                else:
                    stock_code, price = '204001.SH', price_204001

                # 下达股票订单
                xt_trader.order_stock(
                    acc, 
                    stock_code, 
                    xtconstant.STOCK_SELL, 
                    order_volume, 
                    xtconstant.FIX_PRICE, 
                    price, 
                    '国债逆回购策略', 
                    ''
                )
                print(f"成功下达订单，股票代码：{stock_code}，价格：{price}，订单量：{order_volume}。")
            else:
                print("可用资金不足，不进行交易")
        except Exception as e:
            print("下达订单时出现错误:", e)
    else:
        print('连接失败')
```

# 代码注释与解释

首先，代码中的 `place_order_based_on_asset` 函数是整个自动交易策略的核心。该函数首先尝试连接交易平台，并在成功连接后，执行以下步骤：

1. **查询证券资产：** 使用 `xt_trader.query_stock_asset` 函数查询账户的证券资产，特别是可用资金。
    
2. **计算订单量：** 如果可用资金超过1000元，根据资金计算可以购买的国债逆回购数量。
    
3. **获取市场数据：** 通过 `xtdata.subscribe_quote` 和 `xtdata.get_market_data` 函数获取沪深两市一天期国债逆回购的实时报价。
    
4. **价格比较与选择：** 比较两个市场的买一价（`bidPrice`），选择报价更高的市场进行交易。
    
5. **下达交易订单：** 使用 `xt_trader.order_stock` 函数下达卖出订单，执行逆回购操作。
    

# 代码解析

- 通过连接交易系统，获取证券资产信息，判断可用资金是否足够，然后根据资金计算订单量。

- 通过订阅市场数据，获取两支股票的最新买入价，根据价格选择应该交易的股票。

- 最终，通过下达订单实现股票交易。

