## 用途说明

将本地图片上传到指定的 GitHub 仓库，并返回图片的自定义域名 URL。如果图片已存在，则自动重命名后上传。

## 参数

* repo (str): GitHub 仓库名称，格式为 '用户名/仓库名'。
* image_path (str): 本地图像文件的路径。
* commit_message (str, optional): 提交时的说明信息，默认为 "Upload image"。
## 用法

调用 upload_image_to_github(repo, image_path, commit_message) 上传图片并获取图片 URL。

## 示例

```python
image_url = upload_image_to_github('your_username/your_repo', '/path/to/your/image.jpg', 'Upload my image')
print(f"图片已上传至: {image_url}")
```

## 流程图

```mermaid
graph TD
    A[开始] --> B(获取 GitHub Token)
    B --> C{图片是否存在？}
    C -- 不存在 --> D(上传图片)
    C -- 已存在 --> E(重命名图片)
    E --> D
    D --> F(返回图片 URL)
    F --> G(结束)
```

## 代码

```python
import requests
import base64
import os
from datetime import datetime

def upload_image_to_github(repo, image_path, commit_message="Upload image"):
    """
    将图片上传到 GitHub 仓库，如果图片已经存在，则重命名后上传。
    
    :param repo: GitHub 仓库名称，格式为 '用户名/仓库名'。
    :param image_path: 本地图像文件的路径。
    :param commit_message: 提交时的说明信息。
    :return: 上传图片的 URL，带有自定义域名。
    """
    try:
        # 获取 GitHub 令牌，确保你的令牌是正确的
        token = check_account("password", "github_token")

        # 读取图像并将其编码为 base64 格式
        with open(image_path, "rb") as image_file:
            image_data = image_file.read()
            image_base64 = base64.b64encode(image_data).decode('utf-8')

        # 从 image_path 中提取图片文件名和扩展名
        image_name = os.path.basename(image_path)
        name, ext = os.path.splitext(image_name)
        
        # 获取当前日期
        current_date = datetime.now().strftime("%Y%m%d")
        
        # 将文件名重命名为 "原来名字_日期" 的格式
        new_name = f"{name}_{current_date}{ext}"
        path = f"{new_name}"

        # GitHub API 创建或更新文件的 URL
        url = f"https://api.github.com/repos/{repo}/contents/{path}"

        # 准备请求头
        headers = {
            "Authorization": f"token {token}",
            "Accept": "application/vnd.github.v3+json"
        }

        # 检查文件是否存在
        response = requests.get(url, headers=headers)
        counter = 1

        while response.status_code == 200:
            # 文件已存在，增加计数器并修改文件名
            new_name = f"{name}_{current_date}_{counter}{ext}"
            path = f"{new_name}"
            url = f"https://api.github.com/repos/{repo}/contents/{path}"
            response = requests.get(url, headers=headers)
            counter += 1

        # 准备请求数据
        data = {
            "message": commit_message,
            "content": image_base64,
        }

        # 发送请求以上传图片
        response = requests.put(url, headers=headers, json=data)

        if response.status_code in [201, 200]:
            # 返回图片的自定义域名 URL
            custom_domain = "image.sanrenjz.com"
            final_image_name = new_name if counter > 1 else new_name
            return f"https://{custom_domain}/{final_image_name}"
        else:
            # 处理可能的错误
            raise Exception(f"上传图片时出错: {response.json()}")
    
    except Exception as e:
        # 捕获并处理所有异常
        print(f"图片上传失败: {e}")
        return None
```

