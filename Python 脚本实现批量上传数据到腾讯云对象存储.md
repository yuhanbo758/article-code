---
创建时间: 2024-03-12 19:19
修改时间: 2024-03-13 15:55
tags:
  - python
  - 对象存储
  - 效率工具
标题: Python 脚本实现批量上传数据到腾讯云对象存储
share: "true"
---


在现代软件开发和数据管理领域，云存储服务如腾讯云的对象存储（Cloud Object Storage, COS）扮演了极其重要的角色。这些服务不仅提供了一种高效、可扩展的方式来存储和访问数据，而且还支持高并发的数据访问，满足了大数据时代的需求。本文将详细介绍如何使用 Python 脚本将文件和文件夹上传到腾讯云 COS，并将此过程封装为简单的函数，以便于在各种应用中重复使用。

### 腾讯云 COS 简介

腾讯云 COS 是一种分布式存储服务，它允许用户通过网络将数据存储在云端。这种服务支持存储大量数据，并且可以从任何地点、任何设备访问这些数据，非常适合用于网站、移动应用、游戏、视频处理和大数据分析等场景。

### 代码

```python
import sys
import os
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import logging

# 将单个文件上传到cos
def upload_to_cos(bucket, file_name, region='ap-guangzhou', cos_folder='temporary/'):
    """
    上传文件到腾讯云COS指定桶和文件夹中。

    :param bucket: 要上传到的桶名称。
    :param file_name: 本地文件的完整路径。
    :param region: 桶所在的区域，默认为'ap-guangzhou'。
    :param cos_folder: COS中的目标文件夹，默认为'temporary/'。
    """
    # 配置日志
    logging.basicConfig(level=logging.INFO, stream=sys.stdout)

    # 从环境变量中获取secret_id和secret_key
    secret_id = os.environ.get('COS_SECRET_ID')  # 确保已经设置了环境变量COS_SECRET_ID
    secret_key = os.environ.get('COS_SECRET_KEY')  # 确保已经设置了环境变量COS_SECRET_KEY
    token = None  # 使用临时密钥需要传入Token，默认为空,可不填
    scheme = 'https'  # 指定使用 http/https 协议来访问COS，默认为https, 可不填

    # 获取客户端对象
    config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
    client = CosS3Client(config)

    # 从本地文件路径中提取文件名
    base_file_name = os.path.basename(file_name)

    # 上传到COS的路径，包括文件夹和文件名
    cos_path = cos_folder + base_file_name

    # 上传文件
    response = client.upload_file(
        Bucket=bucket,
        LocalFilePath=file_name,
        Key=cos_path,
        PartSize=10,
        MAXThread=10
    )
    print(response['ETag'])



# 配置日志
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 将文件夹上传到cos
def upload_folder_to_cos(bucket, folder_path, region='ap-guangzhou', cos_folder='temporary/'):
    """
    上传文件夹到腾讯云COS指定桶和文件夹中。

    :param bucket: 要上传到的桶名称。
    :param folder_path: 本地文件夹的路径。
    :param region: 桶所在的区域，默认为'ap-guangzhou'。
    :param cos_folder: COS中的目标文件夹，默认为'temporary/'。
    """
    # 配置日志
    logging.basicConfig(level=logging.INFO, stream=sys.stdout)

    # 从环境变量中获取secret_id和secret_key
    secret_id = os.environ.get('COS_SECRET_ID')  # 确保已经设置了环境变量COS_SECRET_ID
    secret_key = os.environ.get('COS_SECRET_KEY')  # 确保已经设置了环境变量COS_SECRET_KEY
    token = None  # 使用临时密钥需要传入Token，默认为空,可不填
    scheme = 'https'  # 指定使用 http/https 协议来访问COS，默认为https, 可不填

    # 获取客户端对象
    config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
    client = CosS3Client(config)

    # 遍历文件夹
    for root, dirs, files in os.walk(folder_path):
        for file_name in files:
            # 从本地文件路径中提取文件名
            base_file_name = os.path.basename(file_name)

            # 上传到COS的路径，包括文件夹和文件名
            cos_path = cos_folder + base_file_name

            # 上传文件
            response = client.upload_file(
                Bucket=bucket,
                LocalFilePath=os.path.join(root, file_name),
                Key=cos_path,
                PartSize=10,
                MAXThread=10
            )
            print(response['ETag'])



# 使用示例
if __name__ == "__main__":
    bucket = 'gdsx-12456638'  # 替换为你的桶名称
    file_name = r"D:\wenjian\python\smart\data\image\csi.png"  # 本地文件的路径
    # 上传单个文件
    upload_to_cos(bucket, file_name)

    
    # folder_path = r"D:\wenjian\python\smart\data\image"  # 本地文件夹的路径
    # 上传整个文件
    # upload_folder_to_cos(bucket, folder_path)
```

### 环境准备

要开始使用 Python 上传文件到 COS，首先需要确保 Python 环境已经安装，并且已经安装了腾讯云 COS 的 Python SDK—— `qcloud_cos`。此外，还需要在腾讯云控制台获取到相应的 `SecretId` 和 `SecretKey`，并将它们保存在环境变量中，以便于脚本中使用。

### 单个文件上传功能

单个文件上传功能通过定义一个名为 `upload_to_cos` 的函数实现。此函数接收四个参数：`bucket`（桶名称），`file_name`（要上传的本地文件路径），`region`（桶所在的区域，默认为'ap-guangzhou'），以及 `cos_folder`（COS 中的目标文件夹，默认为'temporary/'）。

函数内部首先配置日志记录，以便于监控上传过程。然后，它从环境变量中读取 `COS_SECRET_ID` 和 `COS_SECRET_KEY`，并使用这些信息创建一个 `CosConfig` 配置对象和一个 `CosS3Client` 客户端对象。最后，函数使用客户端对象的 `upload_file` 方法将文件上传到指定的 COS 路径。

### 文件夹上传功能

文件夹上传功能通过另一个名为 `upload_folder_to_cos` 的函数实现。与单个文件上传类似，此函数也接收 `bucket`、`folder_path`（本地文件夹路径）、`region` 和 `cos_folder` 四个参数。

不同之处在于，`upload_folder_to_cos` 函数使用 `os.walk` 遍历指定的本地文件夹中的所有文件，并逐一调用 `upload_file` 方法将它们上传到 COS。这使得批量上传文件变得简单高效。

### 使用示例

文章最后提供了两个使用示例，分别展示了如何使用这些函数上传单个文件和整个文件夹到 COS。用户只需替换示例中的 `bucket`、`file_name` 和 `folder_path` 等参数，即可根据自己的需求将数据上传到 COS。

### 小结

通过封装上传功能为函数，本文提供了一种灵活、高效的方法来管理腾讯云 COS 中的数据。这些函数不仅可以用于简单的数据备份，还可以集成到各种应用程序中，为数据存储提供强大的支持。

---

**文章标题建议：**
1. 使用 Python 轻松上传文件到腾讯云 COS
2. Python 脚本实现批量上传数据到腾讯云对象存储
3. 腾讯云 COS 文件上传教程：Python 脚本方法

**文章简介：**
掌握如何使用 Python 将文件和文件夹高

效上传到腾讯云的对象存储服务（COS）。本文详细介绍了上传功能的实现，提供了清晰的代码示例，并解释了如何利用这些代码片段来简化数据管理工作。无论是个人项目还是企业应用，本教程都能帮助您轻松实现云数据存储方案。

