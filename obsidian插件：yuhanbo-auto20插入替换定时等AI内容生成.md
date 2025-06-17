bili 视频：[obsidian插件：yuhanbo-auto2.0，插入、替换、定时等AI内容生成_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1r9NqzzESS/?vd_source=247ac77d4ae7339ea06d0fec09aa8f70)

程序小店：[obsidian插件：auto2.0 AI内容生成 | 三人聚智-余汉波程序小店](https://jy.sanrenjz.com/buy/33)

auto1.0 之前名称为 yuhanbo-ai ，文章视频请前往：[OB插件yuhanbo-ai：快速生成、插入或替换内容 | 余汉波 文档](https://wd.sanrenjz.com/%E4%BB%A3%E7%A0%81%E4%B8%8E%E6%95%88%E7%8E%87/OB%E6%8F%92%E4%BB%B6yuhanbo-ai%EF%BC%9A%E5%BF%AB%E9%80%9F%E7%94%9F%E6%88%90%E3%80%81%E6%8F%92%E5%85%A5%E6%88%96%E6%9B%BF%E6%8D%A2%E5%86%85%E5%AE%B9)

auto1.0 在 github 开源：[yuhanbo758/obsidian-yuhanbo-ai](https://github.com/yuhanbo758/obsidian-yuhanbo-ai)

## 概述

本文档旨在为技术背景的读者提供关于 Obsidian AI 自动插件（版本 2.0.0）的详细解释。该插件由余汉波开发，旨在通过调用 OpenRouter、Deepseek 和 Gemini API 自动生成和替换 Obsidian 文档中的内容。我们将深入探讨插件的功能、结构、算法和潜在改进，并概述其所使用的编程语言和库。

## 插件功能

该插件主要提供以下几个核心功能：

1. 内容生成和替换：允许用户选中一段文本，然后通过 AI 生成的内容替换选中的文本。
1. 内容生成和插入：允许用户选中一段文本，然后将 AI 生成的内容插入到选中文本的后面。
1. 直接生成内容：允许用户直接通过 AI 生成内容，并将内容插入到光标所在位置。
1. 定时任务：允许用户设置定时任务，自动从指定文件读取内容，通过 AI 处理后，保存到指定文件。
1. 快速生成：允许用户设置快捷键，快速通过 AI 生成内容，并将内容插入到光标所在位置。
![](https://xz.sanrenjz.com/image/Pasted%20image%2020250617071818.png?imageSlim)

## 插件结构

该插件主要包含以下几个文件：

* manifest.json：插件的清单文件，包含插件的 ID、名称、版本、描述、作者和是否为桌面应用等信息。
* package.json：Node.js 的包管理文件，包含插件的名称、版本、描述、入口文件、脚本、关键词、作者、许可证、开发依赖和依赖等信息。
* styles.css：插件的样式文件，包含插件的样式定义，用于美化插件的界面。
* main.js：插件的主文件，包含插件的核心逻辑。
### manifest.json

```json
{
  "id": "obsidian-ai-auto",
  "name": "yuhanbo-ai-auto",
  "version": "2.0.0",
  "minAppVersion": "0.15.0",
  "description": "选中内容，定时自动生成内容，调用OpenRouter、Deepseek和Gemini生成内容",
  "author": "余汉波",
  "isDesktopOnly": false
}
```

该文件定义了插件的基本信息，包括插件的 ID（obsidian-ai-auto）、名称（yuhanbo-ai-auto）、版本（2.0.0）、最低 Obsidian 版本（0.15.0）、描述（选中内容，定时自动生成内容，调用OpenRouter、Deepseek和Gemini生成内容）、作者（余汉波）和是否为桌面应用（false）。

### package.json

```json
{
  "name": "obsidian-yuhanbo-ai-auto",
  "version": "2.0.0",
  "description": "Obsidian插件，支持选中内容自动生成、定时任务生成，可调用OpenRouter、Deepseek和Gemini API",
  "main": "main.js",
  "scripts": {
    "dev": "node esbuild.config.mjs",
    "build": "node esbuild.config.mjs production"
  },
  "keywords": ["obsidian", "ai", "openrouter", "deepseek", "gemini", "auto-generate"],
  "author": "余汉波",
  "license": "MIT",
  "devDependencies": {
    "@types/node": "^16.11.6",
    "obsidian": "^0.15.0",
    "esbuild": "0.13.12"
  },
  "dependencies": {
    "moment": "^2.29.4"
  }
}
```

该文件定义了插件的依赖和脚本。其中，main 字段指定插件的入口文件为 main.js。scripts 字段定义了开发和构建插件的脚本。devDependencies 字段定义了开发依赖，包括 @types/node、obsidian 和 esbuild。dependencies 字段定义了插件的依赖，包括 moment。

### styles.css

该文件包含了插件的样式定义，用于美化插件的界面。其中定义了 prompt modal，template list，scheduled task 等组件的样式。

### main.js

main.js 是插件的核心文件，包含了插件的主要逻辑。下面我们将详细分析 main.js 中的代码。

### 默认设置

```javascript
const DEFAULT_SETTINGS = {
    openrouterApiKey: '',
    geminiApiKey: '',
    deepseekApiKey: '',
    defaultModel: 'google/gemini-flash-1.5',
    templatePath: '',
    customModels: [], // 存储用户自定义的模型
    scheduledTasks: [], // 格式: [{id, name, sourcePath, targetPath, model, scheduleType, schedule, dateTime}]
    quickGenerateSettings: [] // 格式: [{id, name, shortcut, model, templatePath, contextLength}]
};
```

DEFAULT_SETTINGS 定义了插件的默认设置，包括 OpenRouter API Key、Gemini API Key、Deepseek API Key、默认模型、模板路径、自定义模型、定时任务和快速生成设置。

### 内置模型列表

```javascript
const BUILT_IN_MODELS = [
    {value: 'deepseek-chat', label: 'deepseek-chat', provider: 'deepseek'},
    {value: 'deepseek-reasoner', label: 'deepseek-reasoner', provider: 'deepseek'},
    {value: 'gemini-2.0-flash', label: 'Gemini 2.0 Flash', provider: 'gemini'},
    {value: 'openai/gpt-4o', label: 'GPT-4O', provider: 'openrouter'},
    {value: 'openai/gpt-4o-mini', label: 'GPT-4O Mini', provider: 'openrouter'},
    {value: 'openai/gpt-4.1-mini', label: 'GPT-4.1 Mini', provider: 'openrouter'},
    {value: 'openai/gpt-4.1-nano', label: 'GPT-4.1 Nano', provider: 'openrouter'},
];
```

BUILT_IN_MODELS 定义了插件的内置模型列表，包括 Deepseek、Gemini 和 OpenRouter 提供的模型。每个模型包含 value、label 和 provider 字段。

### OpenRouterPlugin 类

OpenRouterPlugin 类是插件的主类，继承自 obsidian.Plugin。该类包含了插件的核心逻辑。

### onload 方法

```javascript
async onload() {
    await this.loadSettings();

    this.addCommand({
        id: 'open-openrouter-prompt',
        name: '调用AI生成并替换内容',
        editorCallback: (editor) => {
            const selectedText = editor.getSelection();
            if (selectedText) {
                new PromptModal(this.app, editor, this.settings, 'replace').open();
            } else {
                new obsidian.Notice('请先选择文本');
            }
        }
    });

    this.addCommand({
        id: 'open-openrouter-prompt-insert',
        name: '调用AI生成并插入内容',
        editorCallback: (editor) => {
            const selectedText = editor.getSelection();
            if (selectedText) {
                new PromptModal(this.app, editor, this.settings, 'insert').open();
            } else {
                new obsidian.Notice('请先选择文本');
            }
        }
    });

    this.addCommand({
        id: 'open-openrouter-prompt-direct',
        name: '直接调用AI生成内容',
        editorCallback: (editor) => {
            new PromptModal(this.app, editor, this.settings, 'direct').open();
        }
    });

    this.addSettingTab(new OpenRouterSettingTab(this.app, this));

    // 加载时启动所有定时任务
    this.startAllScheduledTasks();

    // 注册快速生成命令
    this.settings.quickGenerateSettings?.forEach(setting => {
        this.addCommand({
            id: `quick-generate-${setting.id}`,
            name: `快速生成: ${setting.name}`,
            hotkeys: setting.shortcut ? [setting.shortcut] : [],
            editorCallback: async (editor) => {
                await this.handleQuickGenerate(editor, setting);
            }
        });
    });

    // 启动本地服务器
    this.server = http.createServer(async (req, res) => {
        res.setHeader('Access-Control-Allow-Origin', '*');
        res.setHeader('Access-Control-Allow-Methods', 'GET, POST, OPTIONS');
        res.setHeader('Access-Control-Allow-Headers', 'Content-Type');

        if (req.method === 'OPTIONS') {
            res.writeHead(200);
            res.end();
            return;
        }

        if (req.method === 'POST') {
            let body = '';
            req.on('data', chunk => {
                body += chunk.toString();
            });

            req.on('end', async () => {
                try {
                    const data = JSON.parse(body);
                    
                    switch(data.action) {
                        case 'getTemplates':
                            // 获取模板列表
                            console.log('获取模板，路径:', data.path); // 添加日志
                            const templates = await this.getTemplates(data.path, data.searchText || '');
                            console.log('找到的模板:', templates); // 添加日志
                            res.writeHead(200, { 'Content-Type': 'application/json' });
                            res.end(JSON.stringify({ success: true, templates }));
                            break;

                        case 'getTemplateContent':
                            // 获取模板内容
                            const content = await this.getTemplateContent(data.path);
                            res.writeHead(200, { 'Content-Type': 'application/json' });
                            res.end(JSON.stringify({ success: true, content }));
                            break;

                        case 'saveContent':
                            // 保存生成的内容
                            const result = await this.saveGeneratedContent(data.content, data.path);
                            res.writeHead(200, { 'Content-Type': 'application/json' });
                            res.end(JSON.stringify(result));
                            break;

                        default:
                            res.writeHead(400, { 'Content-Type': 'application/json' });
                            res.end(JSON.stringify({ success: false, error: '未知的操作' }));
                    }
                } catch (error) {
                    console.error('处理请求失败:', error);
                    res.writeHead(500, { 'Content-Type': 'application/json' });
                    res.end(JSON.stringify({ success: false, error: error.message }));
                }
            });
        }
    });

    this.server.listen(27123, 'localhost', () => {
        console.log('Obsidian AI 服务器运行在端口 27123');
    });
}
```

onload 方法是插件加载时执行的方法。该方法主要完成以下几个任务：

1. 加载插件设置。
1. 添加三个命令，分别用于调用 AI 生成并替换内容、调用 AI 生成并插入内容和直接调用 AI 生成内容。
1. 添加设置 Tab，用于设置插件的参数。
1. 启动所有定时任务。
1. 注册快速生成命令。
1. 启动本地服务器，用于处理来自其他应用的请求。
### onunload 方法

```javascript
async onunload() {
    // 关闭服务器
    if (this.server) {
        this.server.close();
    }

    // 插件卸载时清理所有定时任务
    this.stopAllScheduledTasks();
}
```

onunload 方法是插件卸载时执行的方法。该方法主要完成以下几个任务：

1. 关闭服务器。
1. 停止所有定时任务。
### startAllScheduledTasks 方法

```javascript
startAllScheduledTasks() {
    if (this.settings.scheduledTasks) {
        this.settings.scheduledTasks.forEach(task => {
            this.startScheduledTask(task);
        });
    }
}
```

startAllScheduledTasks 方法用于启动所有定时任务。该方法会遍历 this.settings.scheduledTasks 数组，然后调用 this.startScheduledTask 方法启动每个定时任务。

### stopAllScheduledTasks 方法

```javascript
stopAllScheduledTasks() {
    this.tasks.forEach(timer => clearInterval(timer));
    this.tasks.clear();
}
```

stopAllScheduledTasks 方法用于停止所有定时任务。该方法会遍历 this.tasks Map，然后调用 clearInterval 方法停止每个定时任务。

### startScheduledTask 方法

```javascript
startScheduledTask(task) {
    if (this.tasks.has(task.id)) {
        clearTimeout(this.tasks.get(task.id));
    }

    const scheduleNextRun = () => {
        const now = new Date();
        let nextRun;

        if (task.scheduleType === 'once') {
            // 单次执行
            nextRun = new Date(task.dateTime);
            if (nextRun <= now) {
                console.log(`任务 "${task.name}" 的执行时间已过期`);
                return; // 不安排执行
            }
        } else {
            // 每天执行
            const [scheduledHour, scheduledMinute] = task.schedule.split(':').map(Number);
            nextRun = new Date(now);
            nextRun.setHours(scheduledHour, scheduledMinute, 0, 0);
            
            if (nextRun <= now) {
                nextRun.setDate(nextRun.getDate() + 1);
            }
        }
        
        const delay = nextRun.getTime() - now.getTime();
        
        const timer = setTimeout(async () => {
            try {
                // 读取源文件内容
                const sourceFile = this.app.vault.getAbstractFileByPath(task.sourcePath);
                if (!sourceFile || !(sourceFile instanceof obsidian.TFile)) {
                    throw new Error(`源文件不存在: ${task.sourcePath}`);
                }
                const content = await this.app.vault.read(sourceFile);

                // 处理内容（与选中发送保持一致的逻辑）
                let contextContent = content;
                
                // 检查是否包含 dataview 查询
                const dataviewRegex = /```dataview\n([\s\S]*?)```/;
                const dataviewMatch = content.match(dataviewRegex);
                
                if (dataviewMatch) {
                    try {
                        const dataviewApi = this.app.plugins.plugins.dataview?.api;
                        if (!dataviewApi) {
                            throw new Error('Dataview 插件未安装或未启用');
                        }
                        
                        const pages = await dataviewApi.query(dataviewMatch[1]);
                        
                        if (pages.successful) {
                            let relatedContent = '';
                            const fileLinks = [];
                            const tableData = pages.value.values;
                            
                            for (const row of tableData) {
                                const link = row.file?.link || row[0];
                                if (link) {
                                    let fileName = link;
                                    if (typeof fileName === 'object' && fileName.path) {
                                        fileName = fileName.path;
                                    }
                                    if (fileName.startsWith('[[') && fileName.endsWith(']]')) {
                                        fileName = fileName.slice(2, -2);
                                    }
                                    fileLinks.push(fileName);
                                }
                            }
                            
                            for (const fileName of fileLinks) {
                                const file = this.app.vault.getFiles().find(f => 
                                    f.basename === fileName || 
                                    f.path === fileName);
                                
                                if (file) {
                                    const fileContent = await this.app.vault.read(file);
                                    relatedContent += `\n---\n## ${file.basename}\n${fileContent}\n`;
                                }
                            }
                            
                            contextContent = contextContent.replace(dataviewMatch[0], 
                                relatedContent ? `数据视图查询结果的相关文章内容：${relatedContent}` : '');
                        }
                    } catch (error) {
                        console.error('处理 Dataview 查询时出错:', error);
                    }
                }
                
                // 处理内链
                const wikiLinkRegex = /\[\[(.*?)\]\]/g;
                const matches = contextContent.match(wikiLinkRegex);
                
                if (matches) {
                    for (const match of matches) {
                        const fileName = match.slice(2, -2);
                        const file = this.app.vault.getFiles().find(f => f.basename === fileName);
                        
                        if (file) {
                            try {
                                const fileContent = await this.app.vault.read(file);
                                contextContent = contextContent.replace(match, 
                                    `${fileName}的内容：\n${fileContent}\n`);
                            } catch (error) {
                                console.error(`读取文件 ${fileName} 失败:`, error);
                            }
                        }
                    }
                }

                // 修改这里：直接传递 model 参数，不需要 context
                const generatedContent = await this.generateAIContent(contextContent, task.model);

                // 生成文件名
                let fileName;
                if (task.customFileName) {
                    fileName = task.customFileName
                        .replace('{YYYY}', nextRun.getFullYear())
                        .replace('{MM}', String(nextRun.getMonth() + 1).padStart(2, '0'))
                        .replace('{DD}', String(nextRun.getDate()).padStart(2, '0'))
                        .replace('{HH}', String(nextRun.getHours()).padStart(2, '0'))
                        .replace('{mm}', String(nextRun.getMinutes()).padStart(2, '0'));
                } else {
                    fileName = [
                        nextRun.getFullYear(),
                        String(nextRun.getMonth() + 1).padStart(2, '0'),
                        String(nextRun.getDate()).padStart(2, '0'),
                        String(nextRun.getHours()).padStart(2, '0'),
                        String(nextRun.getMinutes()).padStart(2, '0')
                    ].join('-');
                }

                const targetPath = `${task.targetPath}/${fileName}.md`;
                
                // 保存生成的内容
                const targetFile = this.app.vault.getAbstractFileByPath(targetPath);
                if (targetFile) {
                    await this.app.vault.modify(targetFile, generatedContent);
                } else {
                    await this.app.vault.create(targetPath, generatedContent);
                }

                new obsidian.Notice(`定时任务 "${task.name}" 执行成功`);

                // 根据任务类型决定是否安排下一次执行
                if (task.scheduleType === 'daily') {
                    scheduleNextRun();
                } else {
                    // 单次执行完成后从置中移除任务
                    const taskIndex = this.settings.scheduledTasks.findIndex(t => t.id === task.id);
                    if (taskIndex !== -1) {
                        this.settings.scheduledTasks.splice(taskIndex, 1);
                        await this.saveSettings();
                    }
                    this.tasks.delete(task.id);
                }
            } catch (error) {
                console.error(`定时任务 "${task.name}" 执行失败:`, error);
                new obsidian.Notice(`定时任务 "${task.name}" 执行失败: ${error.message}`);
                
                if (task.scheduleType === 'daily') {
                    scheduleNextRun();
                }
            }
        }, delay);

        this.tasks.set(task.id, timer);
    };

    scheduleNextRun();
}
```

startScheduledTask 方法用于启动单个定时任务。该方法主要完成以下几个任务：

1. 检查是否已经存在该任务，如果存在，则先停止该任务。
1. 计算下次运行时间。
1. 设置定时器，到下次运行时间时，执行以下操作：
### generateAIContent 方法

```javascript
async generateAIContent(prompt, model) {
    const selectedModelInfo = [...BUILT_IN_MODELS, ...this.settings.customModels]
        .find(m => m.value === model);

    if (!selectedModelInfo) {
        throw new Error('未找到选择的模型');
    }

    // 根据不同的提供商调用相应的 API
    switch (selectedModelInfo.provider) {
        case 'gemini':
            if (!this.settings.geminiApiKey) {
                throw new Error('请先设置 Gemini API Key');
            }
            const geminiResponse = await this.generateWithGemini(prompt, selectedModelInfo.value);
            return geminiResponse.choices[0].message.content;
        case 'deepseek':
            if (!this.settings.deepseekApiKey) {
                throw new Error('请先设置 Deepseek API Key');
            }
            const deepseekResponse = await this.generateWithDeepseek(prompt, selectedModelInfo.value);
            return deepseekResponse.choices[0].message.content;
        case 'openrouter':
        default:
            if (!this.settings.openrouterApiKey) {
                throw new Error('请先设置 OpenRouter API Key');
            }
            const openrouterResponse = await fetch('https://openrouter.ai/api/v1/chat/completions', {
                method: 'POST',
                headers: {
                    'Authorization': `Bearer ${this.settings.openrouterApiKey}`,
                    'Content-Type': 'application/json',
                    'HTTP-Referer': 'http://localhost:8080',
                    'X-Title': 'Obsidian OpenRouter Plugin'
                },
                body: JSON.stringify({
                    model: model,
                    messages: [{
                        role: 'user',
                        content: prompt
                    }]
                })
            });
            const data = await openrouterResponse.json();
            return data.choices[0].message.content;
    }
}
```

generateAIContent 方法用于调用 AI 生成内容。该方法主要完成以下几个任务：

1. 根据模型名称，找到选择的模型信息。
1. 根据不同的提供商，调用相应的 API。
1. 返回 AI 生成的内容。
### generateWithGemini 方法

```javascript
async generateWithGemini(prompt, modelName) {
    // 直接使用模型名称，不需要分割
    const apiEndpoint = `https://generativelanguage.googleapis.com/v1beta/models/${modelName}:generateContent?key=${this.settings.geminiApiKey}`;
    
    try {
        console.log('Calling Gemini API with model:', modelName); // 添加调试日志
        
        const response = await fetch(apiEndpoint, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
            },
            body: JSON.stringify({
                contents: [{
                    parts: [{
                        text: prompt
                    }]
                }]
            });

            if (!response.ok) {
                const errorData = await response.json();
                console.error('Gemini API error response:', errorData); // 添加错误日志
                throw new Error(`Gemini API 错误: ${errorData.error?.message || '未知错误'}`);
            }

            const data = await response.json();
            console.log('Gemini API response:', data); // 添加响应日志
            
            if (!data.candidates || !data.candidates[0] || !data.candidates[0].content) {
                throw new Error('Gemini API 返回了意外的响应格式');
            }

            const generatedText = data.candidates[0].content.parts[0]?.text;
            if (!generatedText) {
                throw new Error('Gemini API 未返回生成的文本');
            }

            return {
                choices: [{
                    message: {
                        content: generatedText
                    }
                }]
            };
        } catch (error) {
            console.error('Gemini API 错误:', error);
            throw error;
        }
    }
```

generateWithGemini 方法用于调用 Gemini API 生成内容。

### generateWithDeepseek 方法

```javascript
async generateWithDeepseek(prompt, model) {
    const response = await fetch('https://api.deepseek.com/v1/chat/completions', {
        method: 'POST',
        headers: {
            'Authorization': `Bearer ${this.settings.deepseekApiKey}`,
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({
            model: "deepseek-chat",
            messages: [
                {"role": "system", "content": "You are a helpful assistant."},
                {"role": "user", "content": prompt}
            ],
            stream: false
        });
    
    if (!response.ok) {
        const errorData = await response.json();
        throw new Error(`DeepSeek API 错误: ${errorData.error?.message || '未知错误'}`);
    }
    
    return await response.json();
}
```

generateWithDeepseek 方法用于调用 Deepseek API 生成内容。

### searchFilePaths 方法

```javascript
 searchFilePaths(query, type = 'all') {
        const files = this.app.vault.getFiles();
        const results = [];
        const queryLower = query.toLowerCase();
        
        // 搜索文件夹
        const folders = new Set();
        files.forEach(file => {
            const parts = file.path.split('/');
            let currentPath = '';
            parts.slice(0, -1).forEach(part => {
                currentPath += (currentPath ? '/' : '') + part;
                if (currentPath.toLowerCase().includes(queryLower)) {
                    folders.add({
                        path: currentPath,
                        type: 'folder',
                        basename: part
                    });
                }
            });
        });

        // 如果只搜索文件夹，直接返回
        if (type === 'folder') {
            return [...folders];
        }

        // 搜索文件
        files.forEach(file => {
            if (file.path.toLowerCase().includes(queryLower)) {
                results.push({
                    path: file.path,
                    type: 'file',
                    basename: file.basename
                });
            }
        });

        return type === 'file' ? results : [...results, ...folders];
    }
```

searchFilePaths 方法用于搜索文件路径。

### handleQuickGenerate 方法

```javascript
 async handleQuickGenerate(editor, setting) {
        const cursor = editor.getCursor();
        const fileContent = editor.getValue();
        const cursorPos = editor.posToOffset(cursor);
        
        // 获取上下文内容
        let contextContent = '';
        if (setting.contextLength > 0) {
            const startPos = Math.max(0, cursorPos - setting.contextLength);
            contextContent = fileContent.substring(startPos, cursorPos);
        }

        try {
            // 读取模板文件
            const templateFile = this.app.vault.getAbstractFileByPath(setting.templatePath);
            if (!templateFile || !(templateFile instanceof obsidian.TFile)) {
                throw new Error(`模板文件不存在: ${setting.templatePath}`);
            }
            const templateContent = await this.app.vault.read(templateFile);

            // 组合提示词
            const prompt = `${templateContent}\n\n上下文内容：\n${contextContent}`;

            // 创建预览元素
            const previewEl = document.createElement('div');
            previewEl.addClass('quick-generate-preview');
            
            // 获取编辑器的容器元素和宽度
            const editorEl = editor.containerEl.querySelector('.cm-content');
            if (!editorEl) {
                throw new Error('无法获取编辑器元素');
            }
            const editorRect = editorEl.getBoundingClientRect();
            
            // 计算预览位置
            const cursorCoords = editor.coordsAtPos(cursor);
            if (!cursorCoords) {
                throw new Error('无法获取光标位置');
            }

            // 设置预览窗口位置和宽度
            previewEl.style.position = 'absolute';
            previewEl.style.left = `${cursorCoords.left}px`;
            previewEl.style.top = `${cursorCoords.bottom}px`;
            previewEl.style.width = `${editorRect.width}px`;
            previewEl.style.maxWidth = `${editorRect.width}px`;
            
            previewEl.setText('正在生成...');
            document.body.appendChild(previewEl);

            // 生成内容
            const generatedContent = await this.generateAIContent(prompt, setting.model);
            
            if (!generatedContent) {
                throw new Error('生成的内容为空');
            }
            
            previewEl.setText(generatedContent);

            // 处理键盘事件
            const handleKeyDown = (e) => {
                if (e.key === 'Tab') {
                    e.preventDefault();
                    // 插入内容
                    editor.replaceRange(generatedContent, cursor);
                    // 计算新的光标位置
                    const newCursor = {
                        line: cursor.line,
                        ch: cursor.ch + generatedContent.length
                    };
                    // 将光标移动到插入内容的末尾
                    editor.setCursor(newCursor);
                }
                // 无论是什么键都移除预览和事件监听
                cleanup();
            };

            // 处理编辑器内容变化
            const handleChange = () => {
                cleanup();
            };

            // 清理函数
            const cleanup = () => {
                document.removeEventListener('keydown', handleKeyDown, true);
                // 使用 Workspace API 移除编辑器的事件监听
                if (this.changeHandler) {
                    this.app.workspace.offref(this.changeHandler);
                    this.changeHandler = null;
                }
                previewEl.remove();
            };

            // 添加事件监听
            document.addEventListener('keydown', handleKeyDown, true);
            // 使用 Workspace API 添加编辑器的事件监听
            this.changeHandler = this.app.workspace.on('editor-change', handleChange);

        } catch (error) {
            console.error('快速生成失败:', error);
            new obsidian.Notice(`快速生成失败: ${error.message}`);
        }
    }
```

handleQuickGenerate 方法用于处理快速生成内容。

### getTemplates 方法

```javascript
    async getTemplates(path, searchText = '') {
        try {
            console.log('搜索模板，路径:', path, '搜索文本:', searchText);
            const templateFolder = this.app.vault.getAbstractFileByPath(path);
            if (!templateFolder) {
                console.log('模板文件夹不存在:', path);
                return [];
            }

            const templates = [];
            const files = this.app.vault.getFiles();
            for (const file of files) {
                if (file.path.startsWith(path) && file.extension === 'md') {
                    // 如果有搜索文本，则进行过滤
                    if (searchText && !file.basename.toLowerCase().includes(searchText.toLowerCase())) {
                        continue;
                    }
                    templates.push({
                        name: file.basename,
                        path: file.path
                    });
                }
            }
            console.log('找到的模板:', templates);
            return templates;
        } catch (error) {
            console.error('获取模板列表失败:', error);
            return [];
        }
    }
```

getTemplates 方法用于获取模板列表。

### getTemplateContent 方法

```javascript
    async getTemplateContent(path) {
        try {
            console.log('获取模板内容，路径:', path);
            const file = this.app.vault.getAbstractFileByPath(path);
            if (!file) {
                throw new Error('模板文件不存在');
            }
            const content = await this.app.vault.read(file);
            return content;
        } catch (error) {
            console.error('获取模板内容失败:', error);
            throw error;
        }
    }
```

getTemplateContent 方法用于获取模板内容。

### saveGeneratedContent 方法

```javascript
 async saveGeneratedContent(content, path) {
        try {
            // 处理路径，移除开头的斜杠
            const folderPath = (path || 'AI_Content').replace(/^\/+/, '');
            const timestamp = new Date().toISOString().replace(/[:.]/g, '-');
            const fileName = `${folderPath}/${timestamp}.md`;

            console.log('准备保存文件:', {
                folderPath,
                fileName,
                vaultPath: this.app.vault.adapter.basePath
            });

            try {
                // 确保文件夹存在
                if (!this.app.vault.getAbstractFileByPath(folderPath)) {
                    await this.app.vault.createFolder(folderPath);
                }

                // 创建文件
                const file = await this.app.vault.create(fileName, content);
                console.log('文件已创建:', file.path);

                // 刷新 Obsidian 视图
                this.app.workspace.trigger('file-created', file);

                return {
                    success: true,
                    path: file.path,
                    fullPath: `${this.app.vault.adapter.basePath}/${file.path}`
                };
            } catch (error) {
                console.error('创建文件失败:', error);
                throw new Error(`创建文件失败: ${error.message}`);
            }
        } catch (error) {
            console.error('保存文件失败:', error);
            throw new Error(`保存文件失败: ${error.message}`);
        }
    }
```

saveGeneratedContent 方法用于保存生成的内容。

### PromptModal 类

PromptModal 类是插件的提示框类，继承自 obsidian.Modal。该类用于显示提示框，让用户输入提示词。

### OpenRouterSettingTab 类

OpenRouterSettingTab 类是插件的设置 Tab 类，继承自 obsidian.PluginSettingTab。该类用于显示设置 Tab，让用户设置插件的参数。

### CustomModelModal 类

CustomModelModal 类是插件的自定义模型模态框类，继承自 obsidian.Modal。该类用于显示自定义模型模态框，让用户添加自定义模型。

### ScheduledTaskModal 类

ScheduledTaskModal 类是插件的定时任务模态框类，继承自 obsidian.Modal。该类用于显示定时任务模态框，让用户添加定时任务。

### QuickGenerateSettingModal 类

