[（加密）QMT与问财结合-单策略：自然语言自动化交易系统 | 三人聚智-余汉波程序小店](https://jy.sanrenjz.com/buy/12)

[（非加密）QMT与问财结合-单策略：自然语言自动化交易系统 | 三人聚智-余汉波程序小店](https://jy.sanrenjz.com/buy/13)

# 使用说明

问财的数据爬取利益于开源库 [zsrl/pywencai: 获取同花顺问财数据](https://github.com/zsrl/pywencai)，但在使用该程序系统需要注意下面几点：

1. 自己部署 python 环境的话，需要安装相应的库，主要有三个，xtquant 、apscheduler 和 pywencai，其他的是标准库，不需安装。 xtquant 是小 QMT 的数据获取和交易的库，可以到官网 [xtquant版本下载 | 迅投知识库 (thinktrader.net)](https://dict.thinktrader.net/nativeApi/download_xtquant.html?id=Xb4724) 自行下载，然后放到你 python 安装所在的 site-packages 文件夹内。apscheduler 和 pywencai 库可以通过 pip 安装，国内镜像可以使用 pip install apscheduler -i https://pypi.tuna.tsinghua.edu.cn/simple。
1. pywencai 库依赖 [Node.js](https://nodejs.org/zh-cn)，自行在电脑中安装安装，否则无法爬取问财数数据。
1. 爬取问财的数据可能出现不稳定，毕竟不是通过 api 获得数据，所以是存在一定的风险的。一旦数据出错或获取不到数据，自动化交易可能带来损失，损失自行承担，概不负责。建议有两个：一、降低爬取频率，以免 IP 被封；二、模拟号充分测试。
## 1. 引言

问财单策略量化交易系统是一款基于自然语言查询的量化交易工具，它允许用户通过简单的自然语言描述来构建交易策略，并自动执行交易操作。本文将深入解析该系统的代码结构、功能实现和工作原理，帮助读者理解这一创新型量化交易工具的技术细节。

## 2. 系统概述

问财单策略量化交易系统主要由以下几个部分组成：

1. 图形用户界面：基于PyQt5构建的交互界面，包含系统设置、策略管理、持仓查询和运行日志四个主要功能区。
1. 问财查询模块：利用pywencai库实现自然语言查询，获取符合条件的证券列表。
1. 交易执行模块：通过xtquant库连接交易接口，执行买入和卖出操作。
1. 定时任务模块：使用schedule库实现策略的定时执行。
1. 日志和数据展示模块：实时显示系统运行状态和交易结果。
## 3. 代码结构分析

### 3.1 导入的库和模块

系统使用了多个Python库来实现不同的功能：

```python
# 标准库
import sys, os, json, random, time
from datetime import datetime, time as datetime_time

# GUI相关
from PyQt5.QtWidgets import (QApplication, QMainWindow, ...)
from PyQt5.QtCore import Qt, QTime, QThread, pyqtSignal

# 数据处理和交易相关
import pywencai
from xtquant.xttrader import XtQuantTrader, XtQuantTraderCallback
from xtquant.xttype import StockAccount
from xtquant import xtconstant, xtdata
import pandas as pd
import math
import schedule
```

这些库可以分为三类：

* 标准库：用于基本的文件操作、时间处理等
* GUI库：PyQt5用于构建图形界面
* 专业库：pywencai用于自然语言查询，xtquant用于交易接口连接，pandas用于数据处理，schedule用于定时任务
### 3.2 核心类结构

系统包含几个核心类：

1. LogRedirector：日志重定向类，将标准输出重定向到GUI界面
1. MyXtQuantTraderCallback：交易回调类，处理交易接口的回调事件
1. TraderThread：交易线程类，在后台执行交易操作
1. WencaiTraderGUI：主窗口类，实现用户界面和交互逻辑
### 3.3 主要功能函数

系统包含多个关键功能函数：

1. place_orders：处理交易委托，执行买入或卖出操作
1. get_stock_price：获取证券实时价格
1. calculate_order_volume：计算委托数量，确保符合交易规则
1. execute_wencai_strategy_with_reserved_cash：执行问财策略，考虑保留现金
## 4. 工作流程详解

### 4.1 系统初始化流程

1. 创建主窗口和GUI组件
1. 加载配置文件（QMT路径、账号等）
1. 初始化日志重定向
1. 设置信号槽连接
### 4.2 交易策略执行流程

1. 用户输入自然语言查询条件（如"涨幅大于5%的转债"）
1. 系统通过pywencai库获取符合条件的证券列表
1. 获取当前持仓，比较新策略和当前持仓的差异
1. 卖出不在新策略中的持仓
1. 计算可用资金（考虑保留现金）
1. 将资金平均分配给需要买入的证券
1. 执行买入委托
1. 更新持仓和资产信息
### 4.3 定时执行机制

系统支持在指定时间自动执行策略：

1. 用户设置执行时间（如14:30）
1. 系统创建定时任务，在指定时间执行策略
1. 定时任务在后台线程中运行，不影响GUI响应
![](https://xz.sanrenjz.com/image/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-03-10%20201149.png?imageSlim)

## 5. 关键算法分析

### 5.1 资金分配算法

系统采用简单的等权资金分配算法：

1. 计算可用资金 = 总资金 - 保留资金
1. 每只证券分配资金 = 可用资金 / 证券数量
1. 根据当前价格计算可买入数量，并向下取整到交易单位（股票为100股，转债为10张）
### 5.2 交易执行算法

系统的交易执行遵循以下原则：

1. 先卖出不在新策略中的持仓
1. 等待卖出委托完成（简单延时）
1. 获取最新资金状况
1. 再买入新策略中的证券
1. 如果没有新证券需要买入，则增持现有持仓
## 6. 用户界面设计

系统界面分为四个主要标签页：

1. 系统设置：配置QMT路径、账号、交易时间等
1. 策略管理：添加和管理问财查询条件，设置定时执行
1. 持仓查询：显示当前持仓和资产信息
1. 运行日志：实时显示系统运行状态和交易结果
界面设计简洁直观，操作流程清晰，适合不同经验水平的用户使用。

![](https://xz.sanrenjz.com/image/OIG3.wyJ.jpg?imageSlim)

## 7. 潜在限制和改进建议

### 7.1 当前限制

1. 单一策略模式：系统只支持一个活跃策略，无法同时运行多个策略
1. 简单资金分配：采用等权分配，没有考虑风险因素和权重优化
1. 交易时机：只在固定时间执行，没有考虑市场波动和最佳交易时机
1. 错误处理：异常处理机制较为简单，可能在复杂情况下不够健壮
1. 回测功能缺失：没有提供策略回测功能，无法评估策略历史表现
### 7.2 改进建议

1. 多策略支持：允许用户创建和管理多个策略，并设置不同的执行条件
1. 智能资金分配：引入风险平价或其他资金分配算法，优化投资组合
1. 动态交易时机：根据市场状况动态决定交易时机，避免不利时段交易
1. 增强错误处理：完善异常处理机制，提高系统稳定性
1. 添加回测功能：集成策略回测模块，帮助用户评估和优化策略
1. 性能优化：优化数据处理和交易执行逻辑，提高系统响应速度
1. 数据可视化：增加图表和可视化功能，直观展示策略表现和市场数据
## 8. 使用的编程语言和库

系统主要使用Python语言开发，依赖以下关键库：

1. PyQt5：用于构建图形用户界面，版本要求 ≥ 5.15.0
1. pywencai：用于问财自然语言查询，版本要求 ≥ 0.3.0
1. xtquant：用于连接交易接口，版本要求 ≥ 1.0.0
1. pandas：用于数据处理和分析，版本要求 ≥ 1.3.0
1. schedule：用于定时任务调度，版本要求 ≥ 1.1.0
