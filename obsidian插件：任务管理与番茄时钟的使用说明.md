插件文档： [obsidian插件：yuhanbo-task，智能任务管理与番茄时钟插件 | 余汉波 文档](https://docs.sanrenjz.com/article/obsidian%E6%8F%92%E4%BB%B6%EF%BC%9Ayuhanbo-task%EF%BC%8C%E6%99%BA%E8%83%BD%E4%BB%BB%E5%8A%A1%E7%AE%A1%E7%90%86%E4%B8%8E%E7%95%AA%E8%8C%84%E6%97%B6%E9%92%9F%E6%8F%92%E4%BB%B6)

## 📋 目录

1. 项目概述
1. 项目结构
1. 核心模块说明
1. 运行环境
1. 安装部署
1. 功能详解
1. API接口说明
1. 配置说明
1. 开发指南
1. 常见问题
## 🎯 项目概述

这是一个为 Obsidian 开发的任务管理和番茄时钟插件，集成了 AI 智能任务拆分功能。插件提供了完整的任务生命周期管理，支持重复性任务和一次性任务，并配备了番茄工作法计时器来提高工作效率。

### 主要特性

* 📝 任务管理: 支持重复性任务（年/月/周/日周期）和一次性任务
* 🍅 番茄时钟: 集成番茄工作法，支持自定义工作和休息时间
* 🤖 AI 智能拆分: 集成 DeepSeek API，自动将复杂任务拆分为子任务
* 📊 进度跟踪: 实时跟踪任务进度和完成状态
* 🔔 智能提醒: 支持自定义提示音和到期提醒
* 📁 文件管理: 自动归档已完成任务到指定文件夹
## 📁 项目结构

```plain text
obsidian-yuhanbo-task/
├── main.js                    # 主程序文件（4007行）
├── manifest.json              # 插件清单文件
├── package.json               # 项目配置文件
├── data.json                  # 用户数据配置文件
├── styles.css                 # 样式文件（412行）
└── README.md                  # 项目说明文档
```

### 文件说明

## 🏗️ 核心模块说明

### 1. YuhanboTaskPlugin (主插件类)

位置: main.js:47-385功能: 插件的入口点，负责初始化和协调各个模块

```javascript
class YuhanboTaskPlugin extends Plugin {
    async onload() {
        // 加载设置、初始化管理器、注册命令等
    }
    
    async onunload() {
        // 清理资源、停止定时器等
    }
}
```

核心方法:

* onload(): 插件加载时的初始化逻辑
* onunload(): 插件卸载时的清理逻辑
* saveSettings(): 保存用户设置
* resetTaskSystem(): 重置任务系统
* startDailyCleanupTimer(): 启动每日清理定时器
* performDailyCleanup(): 执行每日清理任务
### 2. TaskManager (任务管理器)

位置: main.js:1180-2531功能: 核心任务管理逻辑，处理任务的增删改查

```javascript
class TaskManager {
    constructor(plugin) {
        this.plugin = plugin;
        this.tasks = {
            repeating: [],    // 重复性任务
            oneTime: [],      // 一次性任务
            completed: []     // 已完成任务
        };
    }
}
```

核心方法:

* createTask(taskData): 创建新任务
* updateTask(taskId, updates): 更新任务状态
* deleteTask(taskId): 删除任务
* getAllActiveTasks(): 获取所有活跃任务
* loadTasks(): 从文件加载任务
* saveTasks(): 保存任务到文件
* filterRepeatingTasks(): 过滤重复性任务显示
* cleanupExpiredRepeatingTasks(): 清理过期重复性任务
### 3. PomodoroTimer (番茄时钟)

位置: main.js:386-737功能: 番茄工作法计时器实现

```javascript
class PomodoroTimer {
    constructor(plugin) {
        this.plugin = plugin;
        this.state = PomodoroState.IDLE;
        this.timeRemaining = 0;
        this.currentTask = null;
    }
}
```

核心方法:

* startWorkWithTaskSelection(): 开始工作并选择任务
* startWork(task): 开始工作计时
* startBreak(): 开始休息计时
* pause(): 暂停计时器
* resume(): 恢复计时器
* stop(): 停止计时器
* playSound(): 播放提示音
### 4. Modal 类族 (用户界面)

### TaskSelectionModal (任务选择弹窗)

位置: main.js:2532-2675功能: 番茄时钟开始前的任务选择界面

### TaskProgressModal (任务进度弹窗)

位置: main.js:2676-2824功能: 任务进度更新界面

### TaskModal (任务创建/编辑弹窗)

位置: main.js:2825-3584功能: 任务创建和编辑的主界面

### TaskListModal (任务列表弹窗)

位置: main.js:3585-4007功能: 任务列表查看和管理界面

### 5. YuhanboTaskSettingTab (设置页面)

位置: main.js:738-1179功能: 插件设置界面

设置项:

* API 配置 (DeepSeek API Key)
* 任务文件夹路径配置
* 番茄时钟时间配置
* 提示音设置
* AI 功能开关
## 🔧 运行环境

### 基础要求

* Obsidian: 版本 0.15.0 或更高
* 操作系统: Windows / macOS / Linux
* Node.js: 不需要（插件运行在 Obsidian 环境中）
### 依赖项

插件使用 Obsidian 内置的依赖项：

```javascript
const { Plugin, Notice, PluginSettingTab, Setting, Modal, moment, normalizePath } = require('obsidian');
```

* Plugin: Obsidian 插件基类
* Notice: 通知组件
* PluginSettingTab: 设置页面基类
* Setting: 设置项组件
* Modal: 弹窗基类
* moment: 日期处理库
* normalizePath: 路径标准化工具
## 📦 安装部署

### 方法一：手动安装

1. 下载插件文件
1. 启用插件
### 方法二：开发模式安装

1. 克隆代码
1. 重启 Obsidian
### 初始化配置

插件首次启动时会自动：

