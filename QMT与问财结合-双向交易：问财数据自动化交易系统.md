[（加密）QMT与问财结合-双向交易：问财数据自动化交易系统 | 三人聚智-余汉波程序小店](https://jy.sanrenjz.com/buy/10)

[（非加密）QMT与问财结合-双向交易：问财数据自动化交易系统 | 三人聚智-余汉波程序小店](https://jy.sanrenjz.com/buy/11)

视频：[QMT与问财结合-双向交易：问财数据自动化交易系统_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Z4RHYKE9L/?vd_source=247ac77d4ae7339ea06d0fec09aa8f70)

# 使用说明

问财的数据爬取利益于开源库 [zsrl/pywencai: 获取同花顺问财数据](https://github.com/zsrl/pywencai)，但在使用该程序系统需要注意下面几点：

1. 自己部署 python 环境的话，需要安装相应的库，主要有三个，xtquant 、apscheduler 和 pywencai，其他的是标准库，不需安装。 xtquant 是小 QMT 的数据获取和交易的库，可以到官网 [xtquant版本下载 | 迅投知识库 (thinktrader.net)](https://dict.thinktrader.net/nativeApi/download_xtquant.html?id=Xb4724) 自行下载，然后放到你 python 安装所在的 site-packages 文件夹内。apscheduler 和 pywencai 库可以通过 pip 安装，国内镜像可以使用 pip install apscheduler -i https://pypi.tuna.tsinghua.edu.cn/simple。
1. pywencai 库依赖 [Node.js](https://nodejs.org/zh-cn)，自行在电脑中安装安装，否则无法爬取问财数数据。
1. 爬取问财的数据可能出现不稳定，毕竟不是通过 api 获得数据，所以是存在一定的风险的。一旦数据出错或获取不到数据，自动化交易可能带来损失，损失自行承担，概不负责。建议有两个：一、降低爬取频率，以免 IP 被封；二、模拟号充分测试。
## 1. 引言

问财双向委托交易系统是一款基于Python开发的量化交易工具，它结合了问财数据查询与自动化交易执行功能，实现了根据问财查询结果自动买入或卖出股票的功能。本文将深入解析该系统的代码实现，帮助读者理解其工作原理、架构设计和关键算法。

## 2. 系统概述

问财双向委托交易系统主要由以下几个部分组成：

1. 用户界面：基于tkinter构建的图形界面，用于用户输入交易参数和查看交易日志
1. 交易接口：通过xtquant库连接交易服务器，实现股票交易功能
1. 数据查询：使用pywencai库查询问财数据，获取符合条件的股票列表
1. 调度系统：使用apscheduler库实现定时查询和交易功能
1. 交易逻辑：实现买入和卖出的核心算法，包括资金管理、持仓管理等
系统的主要功能包括：

* 根据问财查询结果自动买入或卖出股票
* 支持定时查询和交易
* 可设置买入卖出条件和资金阈值
* 支持多种委托类型和价格调整
* 提供完整的交易日志和状态监控
![](https://xz.sanrenjz.com/image/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-03-10%20171310.png?imageSlim)

## 3. 代码结构分析

### 3.1 类结构

系统主要包含两个类：

1. MyXtQuantTraderCallback：交易回调类，处理交易事件回调
1. WenCaiTrader：主类，实现系统的核心功能
```python
class MyXtQuantTraderCallback(XtQuantTraderCallback):
    # 处理交易回调事件
    
class WenCaiTrader:
    # 实现系统核心功能
```

### 3.2 主要模块和依赖

系统使用了以下主要的Python库：

* tkinter：构建图形用户界面
* xtquant：连接交易服务器，执行交易操作
* pywencai：查询问财数据
* pandas：处理数据结构
* apscheduler：实现定时任务调度
* threading：实现多线程处理
* datetime：处理日期和时间
* json：处理配置文件
## 4. 核心功能实现

### 4.1 交易回调处理

MyXtQuantTraderCallback类继承自XtQuantTraderCallback，实现了多个回调方法来处理交易事件：

```python
def on_stock_order(self, order):
    """委托回报推送"""
    # 处理委托回报

def on_stock_trade(self, trade):
    """成交变动推送"""
    # 处理成交回报

def on_order_error(self, order_error):
    """委托失败推送"""
    # 处理委托失败

def on_cancel_error(self, cancel_error):
    """撤单失败推送"""
    # 处理撤单失败
```

这些回调方法使系统能够实时响应交易事件，记录交易日志，并在必要时采取相应措施。

### 4.2 问财数据查询

系统使用pywencai库查询问财数据，获取符合条件的股票列表：

```python
def get_wencai_data(self, query, query_type_str):
    """从问财获取数据"""
    # 设置查询类型
    query_type_map = {
        "可转债": "conbond",
        "股票": "stock",
        "基金": "fund"
    }
    query_type = query_type_map.get(query_type_str, "stock")
    
    # 查询数据并处理异常
    data = pywencai.get(query=query, query_type=query_type, loop=True)
    
    # 处理查询结果
    # ...
```

该方法实现了以下功能：

1. 根据用户选择的查询品种设置查询类型
1. 添加异常捕获和重试逻辑，提高系统稳定性
1. 提取证券代码和名称，并进行格式化处理
1. 根据证券类型（股票、可转债、基金）进行过滤和格式化
### 4.3 买入订单处理

买入订单处理是系统的核心功能之一，实现了以下逻辑：

```python
def place_buy_order(self, stock_code):
    # 检查交易时间
    # 查询可用资金
    # 撤销未成交订单
    # 获取最新价格
    # 计算当前持仓市值
    # 检查单只证券的总金额限制
    # 计算本次可买金额和委托数量
    # 设置委托价格和类型
    # 执行买入委托
```

买入逻辑包括以下关键步骤：

1. 交易时间检查：确保当前时间在用户设定的买入时间范围内
1. 资金检查：确保可用资金大于保留资金
1. 撤单处理：撤销同一股票的未成交订单，避免重复委托
1. 持仓检查：计算当前持仓市值，确保不超过单只证券的总金额限制
1. 委托数量计算：根据可用资金和单笔买入金额计算委托数量
1. 价格策略：根据用户设置的委托类型和价格调整幅度设置委托价格
1. 委托执行：调用交易接口执行买入委托
### 4.4 卖出订单处理

卖出订单处理与买入类似，但有不同的逻辑：

```python
def place_sell_order(self, stock_code):
    # 检查交易时间
    # 查询可用资金
    # 撤销未成交订单
    # 获取最新价格
    # 计算当前持仓市值
    # 判断是全部卖出还是保留底仓
    # 计算本次卖出数量
    # 设置委托价格和类型
    # 执行卖出委托
```

卖出逻辑的关键步骤包括：

1. 交易时间检查：确保当前时间在用户设定的卖出时间范围内
1. 资金检查：确保可用资金小于资金阈值，避免在资金充足时卖出
1. 持仓检查：确保有可用持仓
1. 卖出策略：根据总卖出金额和单笔卖出金额计算卖出数量，支持保留底仓功能
1. 价格策略：根据用户设置的委托类型和价格调整幅度设置委托价格
1. 委托执行：调用交易接口执行卖出委托
### 4.5 调度系统

系统使用apscheduler库实现定时查询和交易功能：

```python
def init_scheduler(self):
    # 初始化调度器
    
def add_monitor_jobs(self):
    # 添加监控任务
    
def monitor_file(self, query, action):
    # 执行查询和交易
```

调度系统的主要功能包括：

1. 初始化调度器，配置线程池和进程池
1. 添加买入和卖出监控任务，设置查询间隔
1. 定时执行问财查询，获取符合条件的股票列表
1. 根据查询结果执行买入或卖出操作
![](https://xz.sanrenjz.com/image/OIG1.jpg?imageSlim)

## 5. 关键算法分析

### 5.1 资金管理算法

系统实现了精细的资金管理算法，包括：

1. 保留资金：设置保留资金，确保账户始终保留一定的可用资金
1. 单笔交易金额：限制单笔买入或卖出的金额，避免过大的市场冲击
1. 总交易金额：限制单只证券的总买入或卖出金额，实现资金分散
1. 底仓管理：支持保留底仓功能，避免完全清仓
这些算法共同构成了系统的风险控制机制，帮助用户实现科学的资金管理。

### 5.2 价格策略算法

系统支持多种委托类型和价格调整机制：

1. 限价委托：根据最新价格和调整幅度计算委托价格
1. 最优五档：使用市场最优五档价格委托
1. 最优五档转限价：先尝试最优五档，然后转为限价委托
1. 对手方最优：使用对手方最优价格委托
1. 本方最优：使用本方最优价格委托
对于可转债，系统强制使用限价委托，以应对可转债市场的特殊性。

### 5.3 交易时间控制算法

