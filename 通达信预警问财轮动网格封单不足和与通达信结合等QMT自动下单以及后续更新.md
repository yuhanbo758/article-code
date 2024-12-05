## 相关视频

[通达信的预警结合 QMT，实现通达信公式监控自动下单_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1WzsYeXEBa/?vd_source=247ac77d4ae7339ea06d0fec09aa8f70)

[QMT量化实现类似券商的条件单监控委托，封单不足网格等8种条件_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV17B1iYXEiU/?vd_source=247ac77d4ae7339ea06d0fec09aa8f70)

[QMT结合问财，实现自然语言下单，实现定时轮动策略下单_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1XW1WYCEft/?vd_source=247ac77d4ae7339ea06d0fec09aa8f70)

## 策略的委托规则

1. 委托价格非 0，则以限价进行委托
1. 委托价格为 0，委托备注没有“最优五档”，则以最新价进行委托
1. 委托价格为 0，并且备注为“最优五档”，则以对手方的最优五档进行委托，剩余撤销。注意：可转债不支持，会报错。
1. 委托价格为 0，并且备注为“对手方最优”，则以对手方最优进行委托
1. 委托价格为 0，并且备注为“本方最优”，则以本方最优进行委托
## 通达信公式监控：

1. 需自行在通达信建仓两个版块：买入与卖出
1. 板块文件会被存在到通达信软件的 \T0002\blocknew\ 下，需在代码中修改成你的通达信板块路径，比如：
1. 默认“委托数量”=100，即一手，需要修改在调用函数处修改，比如 scheduler.add_job(monitor_file(buy_file_path, "buy", 100), 'interval', seconds=1)。
1. 默认“委托价格“=0，“委托备注”=“最优五档”，即默认以对手方最优五档进行委托。需人修改在 monitor_file 函数中修改。
## 自定义条件监控

1. 即时交易：
1. 上破价：
1. 下破价：
1. 封单不足-注数量：
1. 回落卖-价跌幅-注回撤：
1. 反弹买-价跌幅-注反弹：
1. 价差网格-注价差：
1. 振幅风格-注振幅：
## 问财轮动策略：

1. 运行该模块的必填项：
1. 需区分交易产品，委托备注中尽量带有交易产品的种类，比如 ETF，你要带有“基金”两字，否则可能出错。A 股交易产品包括：
# 包括在内的其他代码+后续更新

1. [可转债轮动策略：近5年年化收益率67.86%，QMT的整体框架+打地鼠+自动逆回购 | 余汉波 文档](https://wd.sanrenjz.com/%E4%BB%A3%E7%A0%81%E4%B8%8E%E6%95%88%E7%8E%87/%20%E5%8F%AF%E8%BD%AC%E5%80%BA%E8%BD%AE%E5%8A%A8%E7%AD%96%E7%95%A5%EF%BC%9A%E8%BF%915%E5%B9%B4%E5%B9%B4%E5%8C%96%E6%94%B6%E7%9B%8A%E7%8E%87%E7%99%BE%E5%88%86%E4%B9%8B67.86%EF%BC%8CQMT%E7%9A%84%E6%95%B4%E4%BD%93%E6%A1%86%E6%9E%B6+%E6%89%93%E5%9C%B0%E9%BC%A0+%E8%87%AA%E5%8A%A8%E9%80%86%E5%9B%9E%E8%B4%AD)
1. [Python打造通达信自动交易系统QMT：突破2%价格笼子限制 | 余汉波 文档](https://wd.sanrenjz.com/%E4%BB%A3%E7%A0%81%E4%B8%8E%E6%95%88%E7%8E%87/Python%E6%89%93%E9%80%A0%E9%80%9A%E8%BE%BE%E4%BF%A1%E8%87%AA%E5%8A%A8%E4%BA%A4%E6%98%93%E7%B3%BB%E7%BB%9F%EF%BC%9A%E7%AA%81%E7%A0%B4%E7%99%BE%E5%88%862%E4%BB%B7%E6%A0%BC%E7%AC%BC%E5%AD%90%E9%99%90%E5%88%B6)
1. [QMT与通达信结合，实现专属量化交易：通达信自动交易系统 | 余汉波 文档](https://wd.sanrenjz.com/%E4%BB%A3%E7%A0%81%E4%B8%8E%E6%95%88%E7%8E%87/QMT%E4%B8%8E%E9%80%9A%E8%BE%BE%E4%BF%A1%E7%BB%93%E5%90%88%EF%BC%8C%E5%AE%9E%E7%8E%B0%E4%B8%93%E5%B1%9E%E9%87%8F%E5%8C%96%E4%BA%A4%E6%98%93%EF%BC%9A%E9%80%9A%E8%BE%BE%E4%BF%A1%E8%87%AA%E5%8A%A8%E4%BA%A4%E6%98%93%E7%B3%BB%E7%BB%9F)
1. [QMT与通达信结合2.0，监测交易系统：通达信自动交易系统 | 余汉波 文档](https://wd.sanrenjz.com/%E4%BB%A3%E7%A0%81%E4%B8%8E%E6%95%88%E7%8E%87/QMT%E4%B8%8E%E9%80%9A%E8%BE%BE%E4%BF%A1%E7%BB%93%E5%90%882.0%EF%BC%8C%E7%9B%91%E6%B5%8B%E4%BA%A4%E6%98%93%E7%B3%BB%E7%BB%9F%EF%BC%9A%E9%80%9A%E8%BE%BE%E4%BF%A1%E8%87%AA%E5%8A%A8%E4%BA%A4%E6%98%93%E7%B3%BB%E7%BB%9F)
### 下载或阅读完整内容为付费内容，金额为：499.9

该内容与微信公众号的付费阅读和本站点的“付费阅读”绑定：

1. 公众号的付费阅读可以直接获得下载或阅读内容，关注微信公众号：余汉波-文章视频-付费阅读，找到对应的内容，或跳转至：[通达信预警、问财轮动、网格、封单不足和与通达信结合等QMT自动下单，以及后续更新](https://mp.weixin.qq.com/s/GAW1SOSnEQ_4q9Zu2fhahw?payreadticket=HMe8F4MwN6iVM1Bh_XBEZot8aAQ7BMFyODo4_vcNL33GYoenDDHonrUWiNrivAGEQJT8tx4)
1. 扫描打赏二维码，打赏指定金额，截图+标题发送至邮箱（yuhanbo@sanrenjz.com），或发送到微信（yuhanbo758），等待回复的付费阅读密码：[1群QMT整体代码+后续更新 | 余汉波 文档](https://wd.sanrenjz.com/%E4%BB%98%E8%B4%B9%E9%98%85%E8%AF%BB/1%E7%BE%A4QMT%E6%95%B4%E4%BD%93%E4%BB%A3%E7%A0%81+%E5%90%8E%E7%BB%AD%E6%9B%B4%E6%96%B0)
![](https://gdsx.sanrenjz.com/PicGo/640.jpg)

