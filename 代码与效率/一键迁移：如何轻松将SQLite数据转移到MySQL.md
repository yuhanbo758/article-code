---
创建时间: 2023-12-13 09:59
修改时间: 2023-12-13 10:47
tags:
  - python
  - 完整代码
标题: 一键迁移：如何轻松将SQLite数据转移到MySQL
share: "true"
profileName: Default
postId: "4042"
categories:
  - 55
---


本段代码提供了一个非常实用的功能：它可以从本地的 SQLite 数据库中读取数据，并将这些数据上传到远程 MySQL 数据库中。这个过程涵盖了数据库连接、数据读取、数据转换和数据上传等多个环节。让我们逐步解析这段代码的每个部分以及它们的作用。

```python
import sqlite3
import pymysql

# 读取本地的sqlite3数据，将它上传到服务器mysql数据。参数有6个，分别是sqlite3路径，sqlite3表名，服务器mysql的ip，mysql用户名，mysql密码，数据表名称
def copy_table_to_mysql(sqlite_db_path: str, table_name: str, mysql_host: str, mysql_user: str, mysql_password: str, mysql_database: str):
    # 连接到SQLite数据库
    sqlite_conn = sqlite3.connect(sqlite_db_path)
    sqlite_cursor = sqlite_conn.cursor()

    # 从SQLite数据库读取数据
    sqlite_cursor.execute(f"PRAGMA table_info({table_name})")
    columns_info = sqlite_cursor.fetchall()
    columns = []
    for column in columns_info:
        column_name = column[1]
        column_type = column[2]
        columns.append(f"`{column_name}` {column_type}")

    columns_str = ', '.join(columns)

    sqlite_cursor.execute(f"SELECT * FROM {table_name}")
    sqlite_data = sqlite_cursor.fetchall()

    # 连接到MySQL数据库
    mysql_conn = pymysql.connect(host=mysql_host,
                                 user=mysql_user,
                                 password=mysql_password,
                                 database=mysql_database)
    mysql_cursor = mysql_conn.cursor()

    # 创建MySQL表格（如果不存在）
    create_table_query = f"CREATE TABLE IF NOT EXISTS `{table_name}` ({columns_str});"
    mysql_cursor.execute(create_table_query)

    # 删除MySQL表中的所有现有记录
    mysql_cursor.execute(f"TRUNCATE TABLE `{table_name}`")

    # 将数据插入到MySQL数据库
    insert_columns_str = ', '.join([f"`{column[1]}`" for column in columns_info])
    insert_query = f"INSERT INTO `{table_name}` ({insert_columns_str}) VALUES ({', '.join(['%s'] * len(columns_info))})"
    mysql_cursor.executemany(insert_query, sqlite_data)

    # 提交更改并关闭连接
    mysql_conn.commit()
    mysql_conn.close()
    sqlite_conn.close()

if __name__ == "__main__":
    # 读取本地的sqlite3数据，将它上传到服务器mysql数据。参数有6个，分别是sqlite3路径，sqlite3表名，服务器mysql的ip，mysql用户名，mysql密码，数据表名称
    copy_table_to_mysql(r'D:\wenjian\python\smart\data\my_data.db', '', '', '', '', '')
```


# 1. 导入必要的模块

代码首先导入了sqlite3和pymysql两个模块。sqlite3模块用于处理SQLite数据库，而pymysql模块则是一个Python客户端，用于连接和操作MySQL数据库。这两个模块是执行数据迁移的关键。

# 2. 定义数据迁移函数

copy_table_to_mysql函数是代码的核心，它接受六个参数，分别是SQLite数据库的路径、表名、MySQL服务器的IP地址、MySQL的用户名、密码和数据库名称。这些参数为数据迁移提供了必要的信息。

# 3. 连接SQLite数据库

函数首先建立与本地SQLite数据库的连接。它通过指定的数据库路径连接到SQLite数据库，并创建一个游标用于执行SQL命令。

# 4. 读取SQLite表结构和数据

接着，函数读取指定SQLite表的结构信息，包括每个字段的名称和类型。然后，它从表中检索出所有数据。这一步是数据迁移的重要组成部分，因为它确保了迁移过程中数据的完整性和结构的一致性。

# 5. 连接MySQL数据库

之后，函数通过pymysql连接到远程MySQL数据库。这一步需要提供MySQL服务器的IP地址、用户名和密码。

# 6. 创建MySQL表并导入数据

在MySQL数据库中，函数首先创建一个与SQLite表结构相同的表。如果表已存在，它不会影响原有表。然后，函数清空MySQL表中的现有数据，并将SQLite中的数据批量插入到MySQL表中。

# 7. 提交更改并关闭数据库连接

最后，函数提交所有更改，并关闭与两个数据库的连接。这保证了数据完整性和连接的安全关闭。

这个过程的优势在于自动化和高效率。它简化了从SQLite到MySQL的数据迁移过程，使得这一任务变得快速且容易。
