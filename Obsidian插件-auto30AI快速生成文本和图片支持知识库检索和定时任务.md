相关文档：

1. [obsidian插件：yuhanbo-auto2.0，插入、替换、定时等AI内容生成 | 余汉波 文档](https://docs.sanrenjz.com/article/obsidian%E6%8F%92%E4%BB%B6%EF%BC%9Aauto2.0%EF%BC%8C%E6%8F%92%E5%85%A5%E3%80%81%E6%9B%BF%E6%8D%A2%E3%80%81%E5%AE%9A%E6%97%B6%E7%AD%89AI%E5%86%85%E5%AE%B9%E7%94%9F%E6%88%90)
1. [Obsidian AI Auto插件：智能笔记的自动化助手，可定时生成内容 | 余汉波 文档](https://docs.sanrenjz.com/article/Obsidian%20AI%20Auto%E6%8F%92%E4%BB%B6%EF%BC%9A%E6%99%BA%E8%83%BD%E7%AC%94%E8%AE%B0%E7%9A%84%E8%87%AA%E5%8A%A8%E5%8C%96%E5%8A%A9%E6%89%8B%EF%BC%8C%E5%8F%AF%E5%AE%9A%E6%97%B6%E7%94%9F%E6%88%90%E5%86%85%E5%AE%B9)
程序小店：[程序小店 - 虚拟商品销售平台](https://shop.sanrenjz.com/product/68df17b123eb0c32a905414c)

## 🎯 项目概述

Obsidian AI 智能助手插件是一个功能强大的 Obsidian 第三方插件，集成了多种 AI 模型和智能功能，支持：

* 内容生成：基于模板和上下文的智能内容生成
* 图片生成：支持多种 AI 图片生成模型
* 知识库管理：智能向量化知识库，支持语义搜索
* 定时任务：自动化内容生成和处理
* 快速生成：自定义快捷键快速生成内容
### 🔧 技术特性

* 多 AI 模型支持：OpenRouter、Deepseek、Gemini、Imagen 等
* 向量化搜索：基于 embedding 的语义搜索
* 实时文件监控：自动更新知识库向量
* 模块化架构：清晰的代码结构，易于扩展
## 📁 目录结构

```plain text
obsidian-yuhanbo-ai-auto2.0/
├── main.js                    # 插件核心代码（3909行）
├── manifest.json              # 插件配置清单
├── styles.css                 # UI样式定义（363行）
├── data.json                  # 用户数据存储
├── 知识库自动更新说明.md        # 知识库功能说明
├── OB插件：AI插件与Templater集成实现笔记自动化处理指南.md
├── 图片生成测试说明.md          # 图片生成功能说明
├── 插件图片生成功能升级总结.md   # 图片功能升级记录
└── Imagen模型修复总结.md        # 模型修复记录
```

## 🏗️ 核心功能模块

### 1. 主插件类 (OpenRouterPlugin)

文件位置: main.js:45-240

核心职责:

* 插件生命周期管理
* 设置加载和保存
* 命令注册和事件监听
* HTTP 服务器启动
关键方法:

* onload(): 插件初始化
* onunload(): 插件卸载清理
* loadSettings(): 加载用户设置
* saveSettings(): 保存用户设置
### 2. AI 内容生成模块

文件位置: main.js:445-585

支持的 AI 提供商:

* Gemini: Google 的生成式 AI 模型
* Deepseek: 深度求索 AI 模型
* OpenRouter: 多模型 API 聚合平台
核心方法:

* generateAIContent(prompt, model): 统一内容生成接口
* generateWithGemini(prompt, modelName): Gemini 模型调用
* generateWithDeepseek(prompt, model): Deepseek 模型调用
### 3. 图片生成模块

文件位置: main.js:500-797

支持的图片模型:

* Imagen 4.0: Google 的图片生成模型
* Gemini Image: Gemini 的图片生成功能
* Veo: 视频生成模型
核心方法:

* generateImage(prompt, model, options): 统一图片生成接口
* generateWithImagen(prompt, config, model): Imagen 模型调用
* generateWithGeminiImage(prompt, config, model): Gemini 图片生成
* saveGeneratedImages(images, baseName): 图片保存处理
### 4. 知识库管理模块

文件位置: main.js:851-1498

核心功能:

* 向量化处理: 将文档转换为向量表示
* 语义搜索: 基于向量相似度的内容检索
* 自动更新: 监控文件变化，自动更新向量
* 增量处理: 只处理变更的文件，节省 API 调用
关键方法:

* createKnowledgeBase(config): 创建知识库
* updateKnowledgeBase(id, forceUpdate): 更新知识库
* searchKnowledgeBase(query, id, topK): 语义搜索
* processFileForKnowledgeBase(file, kb): 文件向量化处理
### 5. 定时任务模块

文件位置: main.js:254-443

功能特性:

* 多种调度类型: 一次性、每日定时
* 模板支持: 基于模板生成内容
* 文件路径解析: 支持 Dataview 查询和文件链接
* 自动文件命名: 支持时间戳和自定义命名
核心方法:

* startAllScheduledTasks(): 启动所有定时任务
* startScheduledTask(task): 启动单个任务
* stopAllScheduledTasks(): 停止所有任务
### 6. UI 界面模块

文件位置: main.js:1822-3909

主要界面组件:

* PromptModal: 内容生成对话框
* ImageGenerationModal: 图片生成对话框
* KnowledgeBaseModal: 知识库配置对话框
* ScheduledTaskModal: 定时任务配置对话框
* OpenRouterSettingTab: 插件设置页面
![](https://gdsx.sanrenjz.com/image/Obsidian%E6%8F%92%E4%BB%B6-auto3.0%EF%BC%9AAI%E5%BF%AB%E9%80%9F%E7%94%9F%E6%88%90%E6%96%87%E6%9C%AC%E5%92%8C%E5%9B%BE%E7%89%87%EF%BC%9A%E6%94%AF%E6%8C%81%E7%9F%A5%E8%AF%86%E5%BA%93%E6%A3%80%E7%B4%A2%E5%92%8C%E5%AE%9A%E6%97%B6%E4%BB%BB%E5%8A%A1_16_9_2560x1440.png?imageSlim)

## 🔧 运行环境

### 必需环境

* Obsidian: 版本 0.15.0 或更高
* 操作系统: Windows/macOS/Linux
* 网络连接: 用于 API 调用
### 可选环境

* Ollama: 本地 AI 模型服务（默认端口 11434）
* Templater 插件: 增强模板功能
## 📦 安装步骤

### 方法 1: 手动安装

1. 下载插件文件
1. 创建插件目录
1. 复制文件
1. 启用插件
### 方法 2: 开发者安装

1. 克隆仓库
