<!-- wp:paragraph -->
<p>这篇文章将深入分析一段 Python 代码，该代码用于从通达信交易平台获取股票行情数据。我们将探讨代码的目的、功能、结构、使用的库、潜在的限制以及改进建议，并提供流程图以帮助理解代码执行过程。</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>python量化分析：打造你的股票分析工具，从通达信数据获取开始_哔哩哔哩_bilibili</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h3>yuhanbolh 库直接调用</h3>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>该代码已经直接封装到个人开源库，可直接调用，不用那么烦琐，如何下面的代码，具体查看 yuhanbolh 文档的：</p>
<!-- /wp:paragraph -->
<!-- wp:code -->
<pre class="wp-block-code"><code class="language-python">

import yuhanbolh as lh

lh.init_global_address(r"D:\jiaoyi\gxtdx\connect.cfg")

df = lh.get_security_bars(9, 0, '000001', 0, 3)
print(df)
</code></pre>
<!-- /wp:code -->
<!-- wp:heading -->
<h3>代码目的和功能</h3>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>这段代码的主要目的是从通达信服务器获取各种类型的股票市场数据，包括盘口数据（买卖五档）、K 线数据、市场股票数量、指数 K 线数据、历史分钟数据、历史分笔成交以及财务数据。</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>它通过连接通达信服务器，发送请求并接收数据，然后将数据转换为 Pandas DataFrame 格式，方便用户进行后续分析和处理。</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h3>代码结构和组织方式</h3>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>代码采用了模块化的设计，主要分为三个函数：</p>
<!-- /wp:paragraph -->
<!-- wp:list {"ordered":true} -->
<ol>
<li>get_tdx_market_address()：负责从通达信配置文件 connect.cfg 中读取服务器 IP 地址和端口号。</li>
<li>get_financial_data()：负责连接通达信服务器，使用指定的函数获取数据，并将数据转换为 Pandas DataFrame。</li>
<li>main 部分（if __name__ == "__main__":）：负责调用上述两个函数，演示如何获取不同类型的市场数据。</li>
</ol>
<!-- /wp:list -->
<!-- wp:paragraph -->
<p>这种模块化的设计提高了代码的可读性和可维护性，方便用户根据需要修改和扩展功能。</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h3>代码中任何复杂或不寻常的方面</h3>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>代码中一个值得注意的方面是 get_financial_data() 函数使用了 lambda 表达式。这使得可以将不同的数据获取函数作为参数传递给 get_financial_data()，从而实现代码的复用。</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>例如，要获取盘口数据，可以传递 lambda api: api.get_security_quotes(...)；要获取 K 线数据，可以传递 lambda api: api.get_security_bars(...)。</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h3>代码的潜在限制和改进建议</h3>
<!-- /wp:heading -->
<!-- wp:list {"ordered":true} -->
<ol>
<li>错误处理:  代码的错误处理机制可以改进。例如，在 get_tdx_market_address() 函数中，如果配置文件不存在或格式错误，应该提供更详细的错误信息，并可以选择使用默认的服务器地址。</li>
<li>异常处理:  get_financial_data() 函数使用了 try...except 块来捕获异常，但这不够精细。应该捕获更具体的异常类型，例如网络连接错误、数据解析错误等，并提供相应的处理逻辑。</li>
<li>重连机制:  如果网络连接中断，代码应该尝试重新连接服务器。</li>
<li>数据校验:  代码没有对接收到的数据进行校验，例如检查数据是否完整、格式是否正确等。</li>
<li>异步处理:  可以使用异步编程来提高数据获取效率，尤其是在需要获取大量数据的情况下。</li>
</ol>
<!-- /wp:list -->
<!-- wp:heading -->
<h3>代码中使用的编程语言和库的简要概述</h3>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>代码使用 Python 编程语言，并依赖于以下库：</p>
<!-- /wp:paragraph -->
<!-- wp:list -->
<ul>
<li>pytdx：用于连接通达信服务器并获取数据。</li>
<li>configparser：用于读取配置文件。</li>
<li>os：用于操作文件系统。</li>
<li>pandas：用于数据处理和分析。</li>
</ul>
<!-- /wp:list -->
<!-- wp:heading -->
<h3>代码流程图 (Mermaid)</h3>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>https://tse3.mm.bing.net/th/id/OIG3.Jco2r0253_spfSFp07mS</p>
<!-- /wp:paragraph -->
<!-- wp:code -->
<pre class="wp-block-code"><code class="language-mermaid">
graph TD
A[开始] --> B{读取配置文件};
B -- 成功 --> C{获取服务器地址};
B -- 失败 --> D[输出错误信息];
C --> E{连接服务器};
E -- 成功 --> F{调用数据获取函数};
E -- 失败 --> G[输出连接失败信息];
F --> H{转换数据为DataFrame};
H --> I[返回DataFrame];
F -- 数据为空 --> J[返回没有收到数据];
G --> K[结束];
D --> K;
J --> K;
I --> K;
</code></pre>
<!-- /wp:code -->
<!-- wp:heading -->
<h3>深入讨论：pytdx库和通达信API</h3>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>pytdx 库是 Python 中用于访问通达信行情数据的关键工具。它封装了通达信的 API 接口，使得开发者可以使用 Python 代码方便地获取股票、期货、期权等市场数据。该库支持多种数据类型，例如实时行情、K 线数据、财务数据等。</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>这段代码中，pytdx.hq.TdxHq_API() 创建了一个 API 对象，用于与通达信服务器进行通信。api.connect() 方法用于建立与服务器的连接，api.disconnect() 方法用于断开连接。其他方法，例如 get_security_quotes()、get_security_bars() 等，用于获取不同类型的市场数据。</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h3>实际应用和扩展</h3>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>这段代码可以作为基础框架，用于构建更复杂的股票分析应用程序。例如，可以结合其他 Python 库，例如 matplotlib 和 seaborn，对获取的数据进行可视化分析。还可以使用机器学习算法对数据进行建模和预测。</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h3>代码</h3>
<!-- /wp:heading -->
<!-- wp:code -->
<pre class="wp-block-code"><code class="language-python">
from pytdx.hq import TdxHq_API
import configparser
import os
import pandas as pd


# 从通达信配置文件获取行情IP地址
def get_tdx_market_address():
    try:
        cfg_file = r"D:\jiaoyi\gxtdx\connect.cfg"
        
        if os.path.exists(cfg_file):
            # 读取配置文件
            config = configparser.ConfigParser()
            with open(cfg_file, 'r', encoding='gb2312') as f:
                config.read_file(f)
            
            # 获取主服务器编号
            primary_host = int(config.get('HQHOST', 'PrimaryHost'))
            
            # 获取对应的服务器信息
            ip_key = f'IPAddress{primary_host:02d}'
            port_key = f'Port{primary_host:02d}'
            
            ip = config.get('HQHOST', ip_key)
            port = int(config.get('HQHOST', port_key))
            print(f"行情服务器地址: {ip}:{port}")
            
            return ip, port
            
    except Exception as e:
        print(f"获取行情地址失败：{str(e)}")
        return None, None

# 处理数据
def get_financial_data(server_ip, server_port, data_function):
    try:
        api = TdxHq_API()

        if api.connect(server_ip, server_port):
            data = data_function(api)  # 使用传入的函数获取数据
            if data is None:
                api.disconnect()
                return "没有收到数据。"

            df = api.to_df(data)  # 转换为DataFrame
            
            api.disconnect()
            return df
        else:
            return "连接失败。"
    except Exception as e:
        return f"发生异常: {str(e)}"


if __name__ == "__main__":
    # 获取行情服务器地址
    ip, port = get_tdx_market_address()

    # 获取盘口数据(买卖五档)，函数api.get_security_quotes；参数为分别为市场代码（0为深，1为沪），股票代码
    # df1 = get_financial_data(ip, port, lambda api: api.get_security_quotes([(0, '000001'),(0,'000002')]))
    # print(df1)

    # 获取K线数据，函数api.get_security_bars；参数为分别为K线类型（0 5分钟K线; 1 15分钟K线; 2 30分钟K线; 3 1小时K线; 4 日K线; 5 周K线; 6 月K线; 7 1分钟; 8 1分钟K线; 9 日K线; 10 季K线; 11 年K线），
    # 市场代码（0为深，1为沪），股票代码，索引（0为最新，1为前一，2为前二），数量
    # df2 = get_financial_data(ip, port, lambda api: api.get_security_bars(9, 0, '000001', 0, 3))
    # print(df2)

    # 获取市场股票数量，函数api.get_security_count；参数为市场代码（0为深，1为沪）
    # df3 = get_financial_data(ip, port, lambda api: api.get_security_count(0))
    # print(df3)

    # 获取指数K线数据，类同获取K线数据，函数api.get_index_bars；参数为分别为K线类型（0为分时，1为1分钟，2为5分钟，3为15分钟，4为30分钟，5为60分钟），
    # 市场代码（0为深，1为沪），指数代码，索引（0为最新，1为前一，2为前二），数量
    # df4 = get_financial_data(ip, port, lambda api: api.get_index_bars(9, 1, '000001', 1, 2))
    # print(df4)

    # 获取历史分钟数据，函数api.get_history_minute_time_data；参数为分别为市场代码（0为深，1为沪），股票代码，日期
    # df5 = get_financial_data(ip, port, lambda api: api.get_history_minute_time_data(0, '000001', 20241115))
    # print(df5)

    # 获取历史分笔成交，函数api.get_transaction_data；参数为分别为市场代码（0为深，1为沪），股票代码，索引（0为最新，1为前一，2为前二），数量
    # df6 = get_financial_data(ip, port, lambda api: api.get_transaction_data(0, '000001', 0, 30))
    # print(df6)

    # 获取财务数据，函数api.get_finance_info；参数为分别为市场代码（0为深，1为沪），股票代码
    df7 = get_financial_data(ip, port, lambda api: api.get_finance_info(0, '000001'))
    pd.set_option('display.max_columns', None)  # 显示所有列
    pd.set_option('display.max_rows', None)     # 显示所有行
    pd.set_option('display.width', None)        # 显示所有宽度
    pd.set_option('display.max_colwidth', None) # 显示所有单元格内容
    print(df7)

</code></pre>
<!-- /wp:code -->
<!-- wp:heading -->
<h3>获取的数据</h3>
<!-- /wp:heading -->
<!-- wp:heading -->
<h4>获取盘口数据(买卖五档)</h4>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>函数 api.get_security_quotes；参数为分别为市场代码（0 为深，1 为沪），股票代码。
get_financial_data(ip, port, lambda api: api.get_security_quotes([(0, '000001'),(0,'000002')]))</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>数据如下：</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h4>获取 K 线数据</h4>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>函数 api.get_security_bars；参数为分别为 K 线类型（0 为分时，1 为 1 分钟，2 为 5 分钟，3 为 15 分钟，4 为 30 分钟，5 为 60 分钟），市场代码（0 为深，1 为沪），股票代码，索引（0 为最新，1 为前一，2 为前二），数量。
get_financial_data(ip, port, lambda api: api.get_security_bars(9, 0, '000001', 0, 3))</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>数据如下：</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h4>获取指数 K 线数据</h4>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>类同获取 K 线数据，函数 api.get_index_bars；参数为分别为 K 线类型（0 为分时，1 为 1 分钟，2 为 5 分钟，3 为 15 分钟，4 为 30 分钟，5 为 60 分钟），市场代码（0 为深，1 为沪），指数代码，索引（0 为最新，1 为前一，2 为前二），数量
get_financial_data(ip, port, lambda api: api.get_index_bars(9, 1, '000001', 1, 2))</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>数据如下：</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h4>获取历史分钟数据</h4>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>函数 api.get_history_minute_time_data；参数为分别为市场代码（0 为深，1 为沪），股票代码，日期。
get_financial_data(ip, port, lambda api: api.get_history_minute_time_data(0, '000001', 20241115))</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>数据如下：</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h4>获取历史分笔成交</h4>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>函数 api.get_transaction_data；参数为分别为市场代码（0 为深，1 为沪），股票代码，索引（0 为最新，1 为前一，2 为前二），数量
get_financial_data(ip, port, lambda api: api.get_transaction_data(0, '000001', 0, 30))</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>数据如下：</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h4>获取财务数据</h4>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>函数 api.get_finance_info；参数为分别为市场代码（0 为深，1 为沪），股票代码
get_financial_data(ip, port, lambda api: api.get_finance_info(0, '000001'))</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>数据如下：</p>
<!-- /wp:paragraph -->
<!-- wp:heading -->
<h4>获取市场股票数量</h4>
<!-- /wp:heading -->
<!-- wp:paragraph -->
<p>函数 api.get_security_count；参数为市场代码（0 为深，1 为沪）
get_financial_data(ip, port, lambda api: api.get_security_count(0))</p>
<!-- /wp:paragraph -->
<!-- wp:paragraph -->
<p>数据如下：</p>
<!-- /wp:paragraph -->