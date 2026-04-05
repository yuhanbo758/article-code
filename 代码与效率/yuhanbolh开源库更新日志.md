### 2024-11-17

1. yuhanbolh 的 0.4.6 版本更新
1. 更新文件为 get_data.py，内容为通过通达信 pytdx 库获取数据
1. init_global_address(cfg_file) 函数为初始化全局服务器地址，cfg_file 参数为自己通达信的配置文件，例如：r"D:\jiaoyi\gxtdx\connect.cfg"
1. get_tdx_market_address(cfg_file) 函数从通达信配置文件获取行情IP地址，不用理会，使用者不用直接调用。
1. get_financial_data(server_ip, server_port, data_function) 数理数据参数，不用理会，使用者不用直接调用。
1. get_security_quotes(market_codes)，获取盘口数据(买卖五档)。market_codes: 列表，每个元素为元组(市场代码,股票代码)，如[(0,'000001'),(0,'000002')]
1. get_security_bars(category, market, code, start, count)，获取K线数据。category: K线类型（0 5分钟K线; 1 15分钟K线; 2 30分钟K线; 3 1小时K线; 4 日K线; 5 周K线; 6 月K线; 7 1分钟; 8 1分钟K线; 9 日K线; 10 季K线; 11 年K线）；market: 市场代码（0:深圳, 1:上海）；code: 股票代码；start: 起始位置（0为最新）count: 数量，最高800。
1. get_security_count(market)，获取市场股票数量。market: 市场代码（0:深圳, 1:上海）。
1. get_index_bars(category, market, code, start, count)，获取指数K线数据。category: K线类型（0:分时, 1:1分钟, 2:5分钟, 3:15分钟, 4:30分钟, 5:60分钟）；market: 市场代码（0:深圳, 1:上海）；code: 指数代码；start: 起始位置（0为最新）；count: 数量
1. get_history_minute_time_data(market, code, date)，获取历史分钟数据。market: 市场代码（0:深圳, 1:上海）；code: 股票代码；date: 日期，格式如20241115。
1. get_transaction_data(market, code, start, count)，获取历史分笔成交。market: 市场代码（0:深圳, 1:上海）；code: 股票代码；start: 起始位置（0为最新）；count: 数量。
1. get_finance_info(market, code)，market: 市场代码（0:深圳, 1:上海）。code: 股票代码。
