---
创建时间: 2023-12-10 10:46
修改时间: 2023-12-10 11:20
tags:
  - python
  - 完整代码
标题: 阿里云AI通义千问api：Python脚本助力内容生成
share: "true"
---


这段代码展示了如何使用 Dashscope 库结合阿里云提供的千问聊天模型（Q-Chat）来自动生成内容。它从 Excel 文件读取提示词和标题，使用这些提示词调用 API 生成文本，然后将生成的内容保存为 Markdown 文件。这种方式对于需要大量内容且希望自动化这一过程的自媒体创作者来说尤其有用。

```python
# For prerequisites running the following sample, visit https://help.aliyun.com/document_detail/611472.html
from http import HTTPStatus
import pandas as pd
import os
import dashscope

dashscope.api_key = ''


def call_with_messages(prompt):
    try:
        messages = [{'role': 'system', 'content': 'You are a helpful assistant.'},
                    {'role': 'user', 'content': prompt}]

        response = dashscope.Generation.call(
            dashscope.Generation.Models.qwen_plus,     # 模型选择
            messages=messages,
            max_tokens=1500,    # 最大字数限制
            top_p=0.8,      # 多样性设置
            repetition_penalty=1.1,     # 重复惩罚设置
            temperature=1.0,      # 随机性设置
            result_format='message',  # 结果格式
        )

        return response
    except Exception as e:
        print(f"生成故事时发生错误: {e}")
        return None

def read_excel_and_generate_stories(file_path, sheet_name, prompt_column, title_column):
    try:
        # 读取Excel文件
        df = pd.read_excel(file_path, sheet_name=sheet_name)
    except Exception as e:
        print(f"读取Excel文件时发生错误: {e}")
        return

    for index, row in df.iterrows():
        try:
            prompt = row[prompt_column]
            title = row[title_column]

            response = call_with_messages(prompt)
            if response and response.status_code == HTTPStatus.OK:
                output = response.output
                if output and output.get("choices"):
                    message = output["choices"][0].get("message")
                    if message:
                        content = message.get("content")

                        # 创建文件名和路径
                        file_name = f'{title}.md'
                        output_path = os.path.join(r'D:\wenjian\obsidian\笔记\自媒体\AI生成', file_name)

                        # 保存到md文件
                        with open(output_path, 'w', encoding='utf-8') as file:
                            file.write(content)
                        print(f'结果已保存到文件：{output_path}')
            else:
                print(f'请求失败，状态码：{response.status_code}')
        except Exception as e:
            print(f"处理Excel行时发生错误: {e}")

if __name__ == '__main__':
    excel_file_path = r"D:\wenjian\onedrive\Desktop\自媒体.xlsx"
    read_excel_and_generate_stories(excel_file_path, '古诗词', '提示词', '名称')
```

# 代码解析

1. **导入必要的库**: 使用http处理HTTP状态。 pandas用于读取和处理Excel文件。 os处理文件和目录路径。 dashscope是一个Python库，用于调用阿里云的聊天生成模型。
2. **设置API密钥**: dashscope.api_key需设置为有效的API密钥。
3. **定义文本生成函数**: call_with_messages函数接收一个提示词，并调用Dashscope的Generation模型生成文本。
4. **读取Excel文件**: read_excel_and_generate_stories函数从Excel文件读取数据，循环遍历每一行，从中提取提示词和标题。
5. **调用API和保存生成的内容**: 对于每一行数据，使用call_with_messages函数生成内容。 若调用成功，将内容保存为Markdown文件。

![](https://mp.toutiao.com/mp/agw/article_material/open_image/get?code=MWU1OGZjYzhjMWUzODc5NDRjZWY0ZDRmNmQ5NmFmMzAsMTcwMjE3NjYxOTkxMw==)

# 代码的实际应用

这个脚本可以在多个领域内发挥作用，例如：

- **自媒体内容创作**：自动生成文章、博客或社交媒体帖子。
- **教育材料制作**：自动生成教育和学习材料。
- **创意写作辅助**：为作家提供创意启发和内容草稿。

# 应用场景

- **内容营销**：快速生成营销文案和故事。
- **个性化产品**：为个性化内容平台生成定制化文本。