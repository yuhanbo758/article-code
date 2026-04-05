[utools插件：余汉波文本片段助手——快速搜索与插入MD文件工具 | 三人聚智-余汉波程序小店](https://jy.sanrenjz.com/buy/23)

github 开源地址：[yuhanbo758/utools-yuhanbo-text: 一个快速搜索并直接插入Markdown文本到当前输入框的uTools插件](https://github.com/yuhanbo758/utools-yuhanbo-text)

# 功能特点和使用方法

一个快速搜索并直接插入 Markdown 文本到当前输入框的 uTools 插件。

## 功能特点

* 自动从指定文件夹加载所有 .md 文件作为文本片段
* 每个 .md 文件名自动注册为 uTools 命令，可直接搜索并插入内容
* 直接在任何应用的输入框中插入 MD 文件内容，无需打开插件界面
* 支持文本片段的创建、编辑、删除
* 支持搜索子文件夹中的文件
* 支持自动插入或复制到剪贴板
* 支持文件变更监控，自动更新命令列表
## 使用方法

1. 在 uTools 中安装本插件“余汉波文本片段助手”
1. 打开插件设置，配置文本片段文件夹路径
1. 在文件夹中创建 .md 文件，或使用插件界面创建文本片段
1. 在任何应用的输入框中，唤起 uTools 并输入 MD 文件名
1. 选择对应的片段，内容将直接插入到当前输入框
例如：如果你有一个名为"感谢信"的 MD 文件，只需在任何输入框中唤起 uTools，输入"感谢信"，选择后内容会自动插入。

## 设置选项

* 文本片段文件夹路径：存放所有 MD 文件的文件夹
* 自动插入内容：选择后直接插入到活动窗口，否则只复制到剪贴板
* 搜索子文件夹：是否包含子文件夹中的文件
## 两种使用模式

1. 直接插入模式（推荐）：
   - 在任何输入框中唤起 uTools

   - 输入文件名，选择对应片段

   - 内容直接插入到当前输入位置

1. 插件管理模式：
   - 通过"文本片段"命令进入插件界面

   - 可以浏览、搜索、新建、编辑、删除文本片段

## 开发说明

本插件基于 uTools API 开发，使用了以下功能：

* 动态特性注册 (utools.setFeature)
* 文件系统操作 (fs 模块)
* 自动化键盘操作 (utools.simulateKeyboardTap)
* 列表模式 (mode: "list")
## 使用提示

* 文件名将作为搜索关键词，建议使用简短且有意义的名称
* 定期刷新插件以更新文件变更
* 对于长文本，建议创建多个小的片段，便于管理和快速找到
![](https://xz.sanrenjz.com/image/uTools%E6%96%87%E6%9C%AC%E7%89%87%E6%AE%B5%E5%8A%A9%E6%89%8B%E5%B7%A5%E4%BD%9C%E6%B5%81%E7%A8%8B%E7%9A%84%E5%9B%BE%E7%89%87%EF%BC%8C%E5%B7%A6%E4%BE%A7%E6%98%BE%E7%A4%BA%E4%B8%80%E4%B8%AA%E6%95%B4%E9%BD%90%E6%8E%92%E5%88%97%E7%9A%84Markdown%E6%96%87%E4%BB%B6%E5%BA%93%EF%BC%8C%E4%B8%AD%E9%97%B4%E6%98%AF%E6%8F%92%E4%BB%B6%E7%9A%84%E6%90%9C%E7%B4%A2%E7%95%8C%E9%9D%A2%EF%BC%8C%E5%8F%B3%E4%BE%A7%E6%98%AF%E6%96%87%E6%9C%AC%E8%87%AA%E5%8A%A8%E6%8F%92%E5%85%A5%E5%88%B0%E8%BE%93%E5%85%A5%E6%A1%86%E7%9A%84%E6%95%88%E6%9E%9C%E3%80%82%E8%83%8C%E6%99%AF%E4%BD%BF%E7%94%A8%E8%93%9D%E8%89%B2%E6%B8%90%E5%8F%98%EF%BC%8C%E7%AA%81%E5%87%BA%E6%8A%80%E6%9C%AF%E6%84%9F%E5%92%8C%E6%95%88%E7%8E%87%E4%B8%BB%E9%A2%98%EF%BC%8C%E9%85%8D%E6%9C%89%E4%BB%A3%E7%A0%81%E7%89%87%E6%AE%B5%E5%92%8CMarkdown%E6%A0%87%E8%AE%B0%E5%85%83%E7%B4%A0%E4%BD%9C%E4%B8%BA%E8%A3%85%E9%A5%B0%E3%80%82.png?imageSlim)

# 简介

## 1. 引言

在日常工作和生活中，我们经常需要重复输入一些固定的文本内容，如问候语、模板回复、代码片段等。如何高效地管理和使用这些文本片段？

uTools余汉波文本片段助手提供了一个优雅的解决方案。本文将深入剖析这个插件的代码实现，向读者展示其工作原理、核心功能和技术细节。

## 2. 插件概述

uTools余汉波文本片段助手是一款基于uTools平台开发的插件，主要功能是帮助用户快速搜索Markdown文件并直接将内容插入到当前的输入框中。该插件具有以下特点：

* 自动扫描指定文件夹中的Markdown文件，将其作为文本片段
* 支持多路径配置，可同时管理多个文件夹中的片段
* 每个Markdown文件名自动注册为uTools命令，支持直接调用
* 支持创建、编辑、删除文本片段的管理功能
* 提供搜索功能，快速定位所需文本片段
* 自动插入功能，无需手动复制粘贴
## 3. 技术架构

该插件采用了HTML、CSS、JavaScript的前端技术栈，结合Electron和uTools API实现了跨平台的功能。整体架构可分为三部分：

1. 前端界面：基于HTML/CSS/JavaScript实现用户交互界面
1. 预加载脚本：使用Node.js提供文件操作、片段管理等功能
1. 插件配置：通过plugin.json定义插件基本信息和命令
### 3.1 文件结构

```plain text
├── index.html       # 前端界面
├── logo.png         # 插件logo
├── plugin.json      # 插件配置文件
├── preload.js       # 预加载脚本，提供核心功能
└── README.md        # 说明文档
```

![](https://xz.sanrenjz.com/image/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202025-04-13%20112745.png?imageSlim)

## 4. 核心功能实现

### 4.1 片段管理与扫描

插件的核心功能是扫描和管理文本片段。这部分主要在preload.js中实现：

```javascript
// 扫描文件夹
function scanFolder() {
    const settings = getSettings();
    const allSnippets = [];
    
    // 获取所有路径
    const paths = Array.isArray(settings.snippetsPaths) && settings.snippetsPaths.length > 0 
        ? settings.snippetsPaths 
        : (settings.snippetsPath ? [settings.snippetsPath] : []);
    
    // 递归扫描函数
    function readDir(dir, subDir = false) {
        if (!settings.searchSubfolders && subDir) {
            // 如果设置不搜索子文件夹，并且当前是子文件夹，则跳过
            return;
        }
        
        const items = fs.readdirSync(dir);
        
        for (const item of items) {
            const fullPath = path.join(dir, item);
            const stat = fs.statSync(fullPath);
            
            if (stat.isFile() && path.extname(item).toLowerCase() === '.md') {
                // 处理Markdown文件
                const content = fs.readFileSync(fullPath, 'utf8');
                const fileName = path.basename(item, '.md');
                
                allSnippets.push({
                    fileName,
                    title: fileName,
                    path: fullPath,
                    content,
                    preview: content.slice(0, 200) + (content.length > 200 ? '...' : '')
                });
            } else if (stat.isDirectory() && settings.searchSubfolders) {
                // 递归处理子文件夹
                readDir(fullPath, true);
            }
        }
    }
    
    // 扫描每个路径
    for (const folderPath of paths) {
        if (folderPath && fs.existsSync(folderPath)) {
            readDir(folderPath);
        }
    }
    
    // 更新缓存和注册动态命令
    snippetsCache = allSnippets;
    registerDynamicCommands(allSnippets);
    
    return allSnippets;
}
```

这段代码实现了递归扫描指定文件夹中的所有Markdown文件，并将它们加载为文本片段。值得注意的是，它支持多路径扫描和子文件夹搜索选项，提供了很好的灵活性。

### 4.2 动态命令注册

插件的一个重要特性是将每个Markdown文件自动注册为uTools命令，这通过registerDynamicCommands函数实现：

```javascript
function registerDynamicCommands(snippets) {
    // 清理旧特性
    const features = utools.getFeatures();
    for (const feature of features) {
        if (feature.code.startsWith('snippet-')) {
            utools.removeFeature(feature.code);
        }
    }
    
    // 定义和注册新特性
    const dynamicFeatures = [];
    
    // 为每个片段创建一个特性
    snippets.forEach(snippet => {
        const featureCode = `snippet-${snippet.fileName}`;
        
        // 准备特性定义
        const feature = {
            code: featureCode,
            explain: `插入文本: ${snippet.fileName}`,
            cmds: [snippet.fileName],
            mode: 'none'
        };
        
        dynamicFeatures.push(feature);
    });
    
    // 批量注册特性
    if (dynamicFeatures.length > 0) {
        utools.setFeature(dynamicFeatures);
    }
}
```

这段代码首先清理了所有以"snippet-"开头的旧特性，然后为每个扫描到的片段创建新的特性定义，并通过uTools API进行注册。这样，用户就可以直接通过文件名调用文本片段。

### 4.3 内容插入功能

插件的另一个核心功能是自动插入内容到当前输入框，这通过insertContent函数实现：

```javascript
function insertContent(content, insertMode = 'plain') {
    try {
        // 1. 隐藏uTools窗口
        utools.hideMainWindow();
        
        if (insertMode === 'plain') {
            utools.copyText(content);
            utools.simulateKeyboardTap('v', 'ctrl');
        } else if (insertMode === 'markdown') {
            // 添加markdown格式的特殊处理
            let formattedContent = content;
            if (!/^#|^\*\*|^>\s|^```|^\-\s|^\d+\.\s/.test(content)) {
                if (content.split('\n').length > 1) {
                    formattedContent = '```\n' + content + '\n```';
                }
            }
            utools.copyText(formattedContent);
            utools.simulateKeyboardTap('v', 'ctrl');
        } else {
            utools.copyText(content);
            utools.simulateKeyboardTap('v', 'ctrl');
        }
        
        // 延时执行，确保界面退出
        setTimeout(() => {
            try {
                utools.simulateKeyboardTap('v', 'ctrl');
                
                setTimeout(() => {
                    utools.outPlugin();
                }, 250);
            } catch (err) {
                utools.showNotification('粘贴失败: ' + err.message);
                utools.outPlugin();
            }
        }, 150);
    } catch (error) {
        utools.showNotification('操作失败: ' + error.message);
        utools.outPlugin();
    }
}
```

这个函数通过一系列巧妙的步骤实现了内容插入：先隐藏uTools窗口，然后将内容复制到剪贴板，模拟Ctrl+V键盘按键实现粘贴，最后退出插件。函数还支持不同的插入模式，可以对Markdown内容进行特殊处理。

### 4.4 用户界面实现

插件的前端界面使用HTML、CSS和JavaScript实现，主要包括三个部分：

1. 片段列表界面：展示所有文本片段，支持搜索和选择
1. 片段编辑界面：用于创建、编辑和删除文本片段
1. 设置界面：配置插件的工作方式
界面设计注重简洁和易用性，采用了现代的CSS样式，包括弹性布局、响应式设计等技术，确保在不同设备上都有良好的体验。

## 5. 数据流与工作流程

### 5.1 插件初始化流程

1. 加载插件配置信息
1. 初始化预加载脚本
1. 扫描指定文件夹，加载所有文本片段
1. 注册动态命令
1. 渲染用户界面
### 5.2 片段插入流程

1. 用户在任何输入框中唤起uTools
1. 输入文件名，选择对应的片段
1. 插件隐藏窗口，将内容复制到剪贴板
1. 模拟Ctrl+V键盘操作，将内容粘贴到输入框
1. 退出插件
## 6. 技术亮点

### 6.1 动态特性注册

插件通过uTools API的动态特性注册功能，将每个Markdown文件自动转化为可调用的命令，大大提高了使用效率。这种实现方式允许用户直接通过文件名调用文本片段，无需额外的搜索步骤。

### 6.2 多路径支持

插件支持同时管理多个文件夹中的文本片段，并提供了默认路径设置，使用户可以更灵活地组织和管理自己的文本片段。

### 6.3 高效的内容插入

