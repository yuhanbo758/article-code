bili 视频：[OB插件-语音助手，讯飞唤醒朗读和听写，语音对生AI生成内容_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1f4xtzZEtt/?vd_source=247ac77d4ae7339ea06d0fec09aa8f70)

github 开源远端地址：[yuhanbo758/obsidian-yuhanbo-voice_assistant: obsidian的语音助手插件，接入讯飞开放平台api](https://github.com/yuhanbo758/obsidian-yuhanbo-voice_assistant)

程序小店：[程序小店 - obsidian插件-语音助手，语音交互、语音合成、唤醒及多种大模型](https://shop.sanrenjz.com/product/68e103718c26cc69cc969957)

亦可到[资源下载 | 余汉波 文档](https://docs.sanrenjz.com/article/%E8%B5%84%E6%BA%90%E4%B8%8B%E8%BD%BD)找到对应的下载链接直接下载。

## 项目概述

Obsidian 语音助手插件 是一个功能完整的语音交互插件，为 Obsidian 笔记软件提供智能语音助手功能。该插件集成了语音识别、语音合成、语音唤醒和多种大语言模型，支持自然语言对话、语音听写、语音朗读等功能。

### 主要特性

* 🎤 语音识别：基于讯飞在线ASR，支持实时语音转文字
* 🔊 语音合成：基于讯飞在线TTS，支持多种音色和语音参数调节
* 🎯 语音唤醒：支持自定义唤醒词，免手动激活
* 🤖 多模型支持：集成Google AI Studio、OpenRouter、讯飞星火等多种大语言模型
* 📝 智能对话：支持持续对话模式和自定义提示词
* ✍️ 语音听写：支持连续语音听写，自动插入笔记
* 📖 语音朗读：支持选中文本的语音朗读功能
* ⚙️ 高度可配置：丰富的配置选项，满足不同使用需求
## 目录结构

```plain text
obsidian-yuhanbo-voice_assistant/
├── main.ts                    # 主插件文件，包含所有核心功能
├── main.js                    # 编译后的JavaScript文件
├── manifest.json              # 插件清单文件
├── package.json               # 项目依赖和脚本配置
├── tsconfig.json              # TypeScript编译配置
├── esbuild.config.mjs         # ESBuild打包配置
├── styles.css                 # 插件样式文件
└── README.md                  # 项目说明文件
```

## 核心功能模块

### 1. 主插件类 (VoiceAssistantPlugin)

* 文件位置: main.ts (第131行开始)
* 功能: 插件的核心控制器，管理所有语音功能
* 主要属性:
### 2. 语音识别模块

* 核心方法: speechToText(), xunfeiOnlineASR()
* 功能: 将音频转换为文字，支持讯飞在线ASR
* 输入: 音频Blob对象
* 输出: 识别的文字字符串
### 3. 语音合成模块

* 核心方法: textToSpeech(), xunfeiOnlineTTS()
* 功能: 将文字转换为语音并播放
* 支持格式: MP3音频流
* 可配置参数: 音色、语速、音量、音调
### 4. 语音唤醒模块

* 核心方法: startWakeListening(), startWakeListeningLoop()
* 功能: 持续监听预设唤醒词，自动激活对话
* 唤醒词: 可自定义，默认包含"你好，小三"等
* 检测间隔: 可配置，默认900毫秒
### 5. 大语言模型集成

* 支持的模型:
* 核心方法: callLLM(), callGoogleAI(), callOpenRouter(), callXunfeiSpark()
### 6. 对话管理模块

* 持续对话: 支持多轮对话，自动管理上下文
* 对话历史: 自动保存对话记录到指定文件夹
* 语音打断: 支持语音打断TTS播放
* 自定义提示词: 支持触发词激活特定提示模板
### 7. 语音听写模块

* 核心方法: startVoiceDictation(), startContinuousDictation()
* 功能: 连续语音转文字，自动插入当前笔记
* 静默检测: 自动检测语音停顿，分段处理
* 实时插入: 识别结果实时插入光标位置
### 8. 设置界面模块

* 类名: VoiceAssistantSettingTab
* 功能: 提供图形化配置界面
* 配置项: 包含所有功能的详细配置选项
![](https://gdsx.sanrenjz.com/image/Obsidian%E6%8F%92%E4%BB%B6-%E8%AF%AD%E9%9F%B3%E5%8A%A9%E6%89%8B%EF%BC%9A%E8%AE%AF%E9%A3%9E%E5%94%A4%E9%86%92%E6%9C%97%E8%AF%BB%E5%92%8C%E5%90%AC%E5%86%99%EF%BC%9A%E8%AF%AD%E9%9F%B3%E5%AF%B9%E7%94%9FAI%E7%94%9F%E6%88%90%E5%86%85%E5%AE%B9_16_9_2560x1440.png?imageSlim)

## 运行环境要求

### 基础环境

* Obsidian: 版本 0.15.0 或更高
* 操作系统: Windows、macOS、Linux (仅桌面版)
* 网络连接: 需要稳定的互联网连接（用于在线语音服务和AI模型调用）
### 开发环境

* Node.js: 16.0 或更高版本
* npm: 6.0 或更高版本
* TypeScript: 4.7.4
* ESBuild: 0.17.3
### 依赖库

```json
{
  "dependencies": {
    "crypto-js": "^4.2.0",
    "ws": "^8.18.3"
  },
  "devDependencies": {
    "@types/crypto-js": "^4.2.2",
    "@types/node": "^16.11.6",
    "typescript": "4.7.4",
    "esbuild": "0.17.3",
    "obsidian": "latest"
  }
}
```

## 安装步骤

### 方法一：手动安装

1. 下载插件文件
1. 安装依赖
1. 编译插件
1. 复制到Obsidian插件目录
### 方法二：开发模式安装

1. 克隆到Obsidian插件目录
1. 安装并构建
1. 在Obsidian中启用插件
## 配置说明

### 基础配置文件 (data.json)

```json
{
  "llmProvider": "xunfei",           // 大语言模型提供商
  "wakeMode": "online",              // 唤醒模式：online/disabled
  "wakeWords": [                     // 自定义唤醒词
    "你好，小三",
    "小三同学", 
    "小三小三"
  ],
  "ttsMode": "online",               // TTS模式：online/disabled
  "asrProvider": "xunfei",           // ASR提供商
  "enableDebugLog": true             // 是否启用调试日志
}
```

### 详细配置项说明

### 1. 大语言模型配置

```typescript
interface LLMConfig {
  llmProvider: 'google' | 'openrouter' | 'xunfei' | 'custom';
  googleApiKey: string;              // Google AI Studio API密钥
  googleModel: string;               // Google模型名称
  openrouterApiKey: string;          // OpenRouter API密钥
  openrouterModel: string;           // OpenRouter模型名称
  xunfeiAppId: string;               // 讯飞应用ID
  xunfeiApiKey: string;              // 讯飞API密钥
  xunfeiApiSecret: string;           // 讯飞API密钥
  xunfeiModel: string;               // 讯飞模型版本
}
```

### 2. 语音功能配置

```typescript
interface VoiceConfig {
  // 语音识别
  asrProvider: 'xunfei';
  
  // 语音合成
  ttsMode: 'disabled' | 'online';
  ttsProvider: 'xunfei';
  ttsVoice: string;                  // 音色选择
  ttsSpeed: number;                  // 语速 (0-100)
  ttsVolume: number;                 // 音量 (0-100)
  ttsPitch: number;                  // 音调 (0-100)
  
  // 语音唤醒
  wakeMode: 'online' | 'disabled';
  wakeWords: string[];               // 唤醒词列表
  autoEnterDialogAfterWake: boolean; // 唤醒后自动进入对话
  wakeDetectionInterval: number;     // 检测间隔(毫秒)
}
```

### 3. 对话功能配置

```typescript
interface DialogConfig {
  continuousDialogDuration: number;     // 持续对话时长(秒)
  showDialogControls: boolean;          // 显示对话控制界面
  conversationSaveFolder: string;       // 对话保存文件夹
  enableVoiceInterruption: boolean;     // 启用语音打断
  customPrompts: Array<{                // 自定义提示词
    name: string;
    trigger: string;
    prompt: string;
    enabled: boolean;
  }>;
}
```

## 使用方法

### 1. 基础语音对话

```typescript
// 通过命令面板启动
// 1. 按 Ctrl+P (Cmd+P) 打开命令面板
// 2. 输入 "开始对话"
// 3. 点击开始语音对话

// 或通过代码调用
this.startVoiceConversation();
```

### 2. 语音唤醒使用

```typescript
// 配置唤醒词
const wakeWords = ["你好，小三", "小三同学", "小三小三"];

// 启动唤醒监听
this.startWakeListening();

// 说出唤醒词后自动激活对话
// 无需手动操作，插件会自动响应
```

### 3. 语音听写功能

```typescript
// 启动语音听写
this.startVoiceDictation();

// 持续听写模式
this.startContinuousDictation();

// 听写内容会自动插入到当前光标位置
```

### 4. 语音朗读功能

```typescript
// 选中文本后启动朗读
this.startVoiceReading();

// 支持暂停/继续/停止控制
this.toggleTTSPlayback();  // 暂停/继续
this.stopTTS();            // 停止朗读
```

### 5. 自定义提示词使用

```typescript
// 在对话中使用触发词
// 例如：说 "提醒我明天开会"
// 会自动应用"任务提醒"提示词模板
```

### 6. 测试功能

插件提供了多个测试方法，可在设置界面的"测试功能"区域使用：

