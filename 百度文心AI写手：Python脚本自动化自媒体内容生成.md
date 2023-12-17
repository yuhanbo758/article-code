---
创建时间: 2023-12-10 11:20
修改时间: 2023-12-10 11:33
tags:
  - python
  - 完整代码
标题: 百度文心AI写手：Python脚本自动化自媒体内容生成
其他: 
share: "true"
profileName: Default
postId: "4030"
categories:
  - 55
---

降低百度文心 4.0 的使用成本：文心 4.0 的 api 调用

下面的代码是一个 Python 脚本，用于自动化地从百度文心 api 生成内容，并将这些内容转换为 Markdown 格式保存。这个过程涉及从 Excel 文件中读取提示词和标题，然后使用这些提示词通过百度 AI 的聊天模型 API 生成文本内容，最后将内容保存为 Markdown 文件，以便在像 Obsidian 这样的笔记应用程序中使用。

```python
import requests
import json
import pandas as pd
import os

# 请确保将 API Key 和 Secret Key 替换为您自己的
api_key = ''
secret_key = ''


def get_access_token(api_key, secret_key):
    try:
        url = "https://aip.baidubce.com/oauth/2.0/token"
        params = {
            "grant_type": "client_credentials",
            "client_id": api_key,
            "client_secret": secret_key
        }
        response = requests.post(url, params=params)
        return response.json().get("access_token")
    except Exception as e:
        print(f"获取access token时发生错误: {e}")
        return None


def get_content(prompt, api_key, secret_key):
    access_token = get_access_token(api_key, secret_key)
    if not access_token:
        print("获取 access token 失败")
        return ""
    try:
        url = "https://aip.baidubce.com/rpc/2.0/ai_custom/v1/wenxinworkshop/chat/completions_pro?access_token=" + access_token
        payload = json.dumps({
            "messages": [
                {
                    "role": "user",
                    "content": prompt
                }
            ],
            # ... 其他参数保持不变
        })
        headers = {
            'Content-Type': 'application/json'
        }
    
        response = requests.request("POST", url, headers=headers, data=payload)
        if response.status_code == 200:
            response_text = response.text.replace("data: ", "")
            response_data = json.loads(response_text)
            content = response_data.get("result")  # 获取结果文本
            if content:
                return content
            else:
                print("未能获取有效内容")
                return ""
        else:
            print(f"请求失败，状态码：{response.status_code}, 响应：{response.text}")
            return ""
    except Exception as e:
        print(f"请求过程中发生错误: {e}")
        return ""
get_content("你好", api_key, secret_key)

def main(api_key, secret_key):
    try:
        file_path = r"D:\wenjian\onedrive\Desktop\自媒体.xlsx"
        df = pd.read_excel(file_path, sheet_name='古诗词')

        for index, row in df.iterrows():
            prompt = row['提示词']
            title = row['名称']
            content = get_content(prompt, api_key, secret_key)
            file_name = f'{title}.md'
            output_path = os.path.join(r'D:\wenjian\obsidian\笔记\自媒体\AI生成', file_name)

            with open(output_path, 'w', encoding='utf-8') as file:
                file.write(content)
            print(f'结果已保存到文件：{output_path}')
    except Exception as e:
        print(f"处理Excel文件或保存Markdown时发生错误: {e}")


if __name__ == '__main__':
    main(api_key, secret_key)
```

# 代码解析

1. **导入必要的库**: 使用requests库来处理HTTP请求。 使用json来处理JSON数据。 pandas用于读取和处理Excel文件。 os库用于文件路径操作。
2. **获取访问令牌**: get_access_token函数通过提供API密钥和密钥获取访问令牌。
3. **生成内容**: get_content函数接收用户的提示词，并发送到百度AI平台获取生成的文本。
4. **读取Excel文件**: 在main函数中，使用pandas读取Excel文件中的提示词和标题。
5. **调用API生成内容并保存文件**: 对于每个提示词，调用get_content函数，并将返回的内容保存为Markdown文件。

![](https://mp.toutiao.com/mp/agw/article_material/open_image/get?code=NTA0NGRlNWUxNTgxMWQwOTk2ZmNkYzY3NTUxYWM4NmIsMTcwMjE3ODY2MjgyOQ==)

# 代码的实际应用

这个脚本适用于需要创建大量文本内容的场景，例如：

- **自媒体运营**：自动生成文章、帖子或其他内容。
- **教育内容创建**：为教学和学习材料自动生成文本。
- **内容营销**：为营销材料自动生成文案和故事。

# 应用场景

- **个性化内容生成**：为用户提供定制化的内容体验。
- **自动化写作**：帮助作者和编辑自动化创作过程。
