---
创建时间: 2023-12-10 11:46
修改时间: 2023-12-10 11:51
tags:
  - python
  - 完整代码
标题: 一键转换：使用OpenAI的Python脚本制作语音文件
其他: 
profileName: Default
postId: "4026"
categories:
  - 55
share: "true"
---


这段 Python 代码演示了如何使用 OpenAI 的文本转语音（TTS）服务，将文本转换成语音并保存为音频文件。该脚本通过定义一个函数 generate_speech 来实现这一过程，该函数接收文本、语音模型、选定的声音和文件保存路径作为参数。

```python
from pathlib import Path
from openai import OpenAI
# api文档:https://platform.openai.com/docs/guides/text-to-speech
# 可以将独立与对话分开成两个语音，同时

def generate_speech(api_key, text, model, voice, file_path):
    """
    使用 OpenAI 的 TTS 生成语音，并保存到指定路径。

    :param api_key: OpenAI 的 API 密钥。
    :param text: 要转换为语音的文本。
    :param voice: 选择的语音模型。
    :param file_path: 保存语音文件的路径。
    :return: 保存文件的路径。
    """
    client = OpenAI(api_key=api_key)

    response = client.audio.speech.create(
      model=model,
      voice=voice,
      input=text
    )

    path = Path(file_path)
    with open(path, 'wb') as file:
        file.write(response.content)

    return f'文件已保存到: {path}'

# 使用示例
api_key = ''
text = "您要转换的文本"
model="tts-1"   # tts-1、tts-1-hd、tts-1、tts-1-hd
voice = "shimmer"  # alloy、echo、fable、onyx、nova、shimmer
file_path = r"D:\wenjian\临时\speech.mp3"

print(generate_speech(api_key, text, model, voice, file_path))
```

# 代码解析

1. **导入必要的模块**: Path用于处理文件路径。 OpenAI用于调用OpenAI的API。
2. **函数定义**: generate_speech函数负责调用OpenAI的TTS服务。
3. **API调用**: 使用audio.speech.create方法生成语音，将文本转换为语音。
4. **保存文件**: 打开指定路径的文件，并将生成的语音内容写入该文件。
5. **使用示例**: 提供API密钥、待转换文本、模型、声音类型和文件路径。

![](https://mp.toutiao.com/mp/agw/article_material/open_image/get?code=MDY0YWNkMjVlZDhmYTU2NWViZDg1NzUyZGU1NTgyNDYsMTcwMjE4MDExMzQ5NA==)

# 代码的实际应用

这个脚本可以被用于多种需要语音输出的场景，包括：

- **无障碍应用**：为视障人士阅读文本内容。
- **自动化系统**：语音提示和用户交互。
- **内容制作**：生成有声读物和多媒体内容。

# 应用场景

- **教育**：为在线课程和培训材料创建语音内容。
- **娱乐**：制作有声书和播客。
