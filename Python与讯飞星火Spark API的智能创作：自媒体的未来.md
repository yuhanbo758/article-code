---
创建时间: 2023-12-10 11:34
修改时间: 2023-12-10 11:46
tags:
  - python
  - 完整代码
标题: Python与讯飞星火Spark API的智能创作：自媒体的未来
share: "true"
profileName: Default
postId: "4036"
categories:
  - 55
---


这段 Python 代码是一个自动化脚本，用于读取 Excel 文件中的数据，并使用 讯飞星火 Spark API 来生成基于给定提示词的文本内容。生成的内容随后被保存为 Markdown 文件，这可以用于内容创作，特别是在自媒体领域。

```python
import SparkApi
import pandas as pd
import os

#以下密钥信息从控制台获取
appid = ""     #填写控制台中获取的 APPID 信息
api_secret = ""   #填写控制台中获取的 APISecret 信息
api_key =""    #填写控制台中获取的 APIKey 信息


# 配置参数
domain = "generalv3"   # v3.0版本
temperature = 0.5
top_k = 4
max_tokens = 8192  # 最大生成长度为8192

# 云端环境的服务地址
Spark_url = "wss://spark-api.xf-yun.com/v3.1/chat"  # v3.0环境的地址

text = []

def getText(role, content):
    """添加消息到列表中"""
    text.append({"role": role, "content": content})
    return text

def getLength(text):
    """计算消息列表的总长度"""
    return sum(len(content["content"]) for content in text)

def checkLength(text):
    """确保消息列表总长度不超过8000字符"""
    while getLength(text) > 8000:
        del text[0]
    return text

def callSparkApi(question):
    """调用 Spark API 并获取回答"""
    try:
        SparkApi.answer = ""
        SparkApi.main(appid, api_key, api_secret, Spark_url, domain, question)
        return SparkApi.answer
    except Exception as e:
        print(f"调用 Spark API 时出现错误: {e}")
        return None

def readExcelAndGenerateOutput(file_path, sheet_name, prompt_column, title_column):
    """读取 Excel 文件，并对每行数据调用 Spark API，然后保存结果为 Markdown 文件"""
    try:
        df = pd.read_excel(file_path, sheet_name=sheet_name)
    except Exception as e:
        print(f"读取 Excel 文件时出现错误: {e}")
        return

    for index, row in df.iterrows():
        try:
            prompt = row[prompt_column]
            title = row[title_column]

            text.clear()
            question = checkLength(getText("user", prompt))
            answer = callSparkApi(question)
            getText("assistant", answer)

            if answer:
                # 创建文件名和路径
                file_name = f'{title}.md'
                output_path = os.path.join(r'D:\wenjian\obsidian\笔记\自媒体\AI生成', file_name)

                # 保存到 Markdown 文件
                with open(output_path, 'w', encoding='utf-8') as file:
                    for item in text:
                        file.write(item["role"] + ": " + item["content"] + "\n\n")
                print(f'结果已保存到文件：{output_path}')
        except Exception as e:
            print(f"处理 Excel 行数据时出现错误: {e}")

if __name__ == '__main__':
    excel_file_path = r"D:\wenjian\onedrive\Desktop\自媒体.xlsx"
    readExcelAndGenerateOutput(excel_file_path, '古诗词', '提示词', '名称')
```

# 代码解析

1. **引入所需模块**: SparkApi用于调用Spark API进行文本生成。 pandas用于读取Excel文件。 os用于文件路径和文件操作。
2. **设置API密钥信息**: appid, api_secret, api_key从控制台获取并填入。
3. **定义全局变量和函数**: text列表存储对话历史。 getText添加对话到列表。 getLength计算对话列表总长度。 checkLength保持对话长度在限制内。
4. **API调用**: callSparkApi函数利用SparkApi模块调用API并获取回答。
5. **处理Excel数据并生成文件**: readExcelAndGenerateOutput函数读取Excel中的提示词和标题，生成内容，并将其保存为Markdown文件。

![](https://mp.toutiao.com/mp/agw/article_material/open_image/get?code=NzM2NjY4NGQ4MzViMTYyYWFmNTc2MDUzODY1ZWVhYzUsMTcwMjE3OTQ3NzM5Nw==)

# 代码的实际应用

此脚本可用于各种需要大量文本内容的场景：

- **自媒体运营**: 自动生成博客文章、社交媒体帖子。
- **内容创作**: 利用AI生成故事、文章等。
- **教育资源**: 自动生成教育材料和教案。

# 应用场景

- **自动化营销**：为广告和营销材料快速生成文案。
- **知识库构建**：创建知识库和帮助文档。
