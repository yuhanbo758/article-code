---
创建时间: 2024-03-15 16:47
修改时间: 2024-03-15 17:09
tags:
  - python
  - AI
  - gpt
  - 效率工具
标题: 3分钟构建本地GPT，不用GPU，家用办公电脑便可构建
share: "true"
---
[ollama/ollama：使用 Llama 2、Mistral、Gemma 和其他大型语言模型启动并运行。 (github.com)](https://github.com/ollama/ollama)
### 安装 Ollama

- 转到 Ollama 网站
- 单击“下载”。
- 选择与您的操作系统匹配的安装程序。
- 按照安装向导进行操作。

### 安装模型
安装完 **Ollama** 后，你可以按照以下步骤来安装模型并运行：

1. **安装 Ollama 模型**：
    
    - 首先，确保你已经成功安装了 Ollama。如果你还没有安装，请参考之前的步骤。
    - 打开终端或命令行界面。
2. **下载模型**：
    
    - Ollama 提供了一系列预构建的模型，你可以从 Ollama 模型库中选择一个。
    - 例如，你可以下载 Llama 2 模型：
        
        ```bash
        ollama download llama2
        ```
        
        这将下载 Llama 2 模型并将其安装到本地。
3. **运行模型**：
    
    - 下载完模型后，你可以使用以下命令来运行它：
        
        ```bash
        ollama run llama2
        ```
        
        这将启动 Llama 2 模型并等待输入。
    - 输入你想要模型生成的文本，然后按下回车键。
4. **获取模型输出**：
    
    - 模型会生成一个文本输出，你可以在终端或命令行界面中看到。
    - 如果你想将输出保存到文件中，可以使用重定向操作符 `>`：
        
        ```bash
        ollama run llama2 > output.txt
        ```
        
        这将把模型的输出保存到名为 `output.txt` 的文件中。
5. **自定义模型参数**（可选）：
    
    - Ollama 允许你自定义模型的参数，例如温度、生成的文本长度等。
    - 查阅 Ollama 文档以获取更多关于自定义参数的信息。

### python 调用
```python
import ollama

def ask_question(question):
    response = ollama.chat(model='gemma:7b', messages=[{'role': 'user', 'content': question}])
    return response['message']['content']

# 使用函数
print(ask_question("你能干吗"))
```


ollama rm llama2 为删除命令

请注意，这里的示例是基于 Llama 2 模型的。你可以根据需要选择其他模型，并按照类似的步骤进行操作。祝你在使用 Ollama 进行模型生成时玩得愉快！🚀


```
ollama pull mistral
ollama pull nomic-embed-text
# Remember to close the Ollama app first to free up the port
set OLLAMA_ORIGINS=app://obsidian.md*
ollama serve
```