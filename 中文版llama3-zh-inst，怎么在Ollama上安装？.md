---
创建时间: 2024-05-04 22:25
修改时间: 2024-05-06 17:10
tags:
  - gpt
  - AI
  - 效率工具
share: "true"
link: https://yuhanbo.notion.site/llama3-zh-inst-Ollama-65c90806cc8d497aa9b320573b5db958
notionID: 65c90806-cc8d-497a-a9b3-20573b5db958
---


### 1. 下载应用程序

根据操作系统（macOS、Windows、Linux）从 [ollama官网](https://ollama.com/download) 下载软件。确保下载版本为 v0.1.33 或更高，以避免无限生成问题。

### 2. 安装 Ollama

**macOS：**

* 下载后直接拖入“应用程序”。

**Windows 预览版：**

* 下载并运行 exe 文件。

**Linux：**

* 执行以下命令：

```
curl -fsSL https://ollama.com/install.sh | sh
```

![OIG2.jpg](https://gdsx.sanrenjz.com/PicGo/OIG2.jpg)


### 3. 创建 Modelfile 文件

首先你要到 [Hugging Face](https://huggingface.co/hfl/llama-3-chinese-8b-instruct-gguf) 或 [ModelScope](https://modelscope.cn/models/ChineseAlpacaGroup/llama-3-chinese-8b-instruct-gguf) 下载 GGUF 文件，然后才是下面的安装配置。

Chinese-LLaMA-Alpaca-3开源项目 [ymcui/Chinese-LLaMA-Alpaca-3: 中文羊驼大模型三期项目 (Chinese Llama-3 LLMs) developed from Meta Llama 3 (github.com)](https://github.com/ymcui/Chinese-LLaMA-Alpaca-3) 或

在文本编辑器中编写 Modelfile 文件，内容示例如下：

```yaml
FROM /your-path-to-ggml/ggml-model-q8_0.gguf
TEMPLATE """{{ if .System }}<|start_header_id|>system<|end_header_id|>

{{ .System }}<|eot_id|>{{ end }}{{ if .Prompt }}<|start_header_id|>user<|end_header_id|>

{{ .Prompt }}<|eot_id|>{{ end }}<|start_header_id|>assistant<|end_header_id|>

{{ .Response }}<|eot_id|>"""
SYSTEM """"""
PARAMETER num_keep 24
PARAMETER stop <|start_header_id|>
PARAMETER stop <|end_header_id|>
PARAMETER stop <|eot_id|>
PARAMETER stop assistant
PARAMETER stop Assistant
```

* `FROM` 字段指向 GGUF 文件的路径，使用的是 Instruct 模型。
* `TEMPLATE` 字段定义了指令模板格式。

### 4. 创建模型实例

在命令行中运行以下命令，创建一个名为 `llama3-zh-inst`（名称可自定义）的模型实例，加载 Modelfile 配置：

```
ollama create llama3-zh-inst -f Modelfile
```

比如我的 Modelfile 文件放在 `D:\xiazai\edge\Modelfile`，那我我要运行的就是 `ollama create llama3-zh-inst -f D:\xiazai\edge\Modelfile'

命令行将输出 "success"，表示创建成功。

### 5. 开始聊天

通过运行以下命令进入聊天程序：

```
ollama run llama3-zh-inst
```

在出现的 `>>>` 后输入用户指令；输入 `/bye` 结束聊天。


