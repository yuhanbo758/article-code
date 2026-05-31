bili 视频 1：[小白Python工具：余汉波程序控制工具_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1QLPcexEsK/?vd_source=247ac77d4ae7339ea06d0fec09aa8f70)

bili视频 2：[小白也能使用的python工具，开箱即用量化程序，内含QMT通达信监控交易_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1HJp8zhEyE/?vd_source=247ac77d4ae7339ea06d0fec09aa8f70)

版本下载：[三人聚智-余汉波 - sanrenjz](https://www.sanrenjz.com/sanrenjz/)

开源地址：[yuhanbo758/yuhanbopy-app: 三人聚智-Python程序管理工具](https://github.com/yuhanbo758/yuhanbopy-app)

程序小店：[程序小店 - 虚拟商品销售平台](https://shop.sanrenjz.com/)

# 使用方法

## 1. 下载与安装

在 [sanrenjz - 三人聚智-余汉波](https://www.sanrenjz.com/sanrenjz/)的版本介绍中找到你需要版本，然后进行下载解压，解压之后双击“三人聚智-余汉波程序控制工具.exe”便可运行程序，绿色版本，不需安装。QMT 量化建议安装 yuhanbopy-lh 版本，也是 github 开源版本，嵌入 QMT 相关库。

![](https://xz.sanrenjz.com/image/Pasted%20image%2020260531162143.png?imageSlim)

若是 QMT 量化交易的小白建议 yuhanbopy-lh 版本，该版内嵌 python 和 mini QMT 的库 xquant，省略复杂的配置。

因为应用是嵌入 python 和 xquant 库的，解压后有近 900M，下载消耗的资源较多，每次下载，这边需向腾讯云支付约 0.2 元。所以，为减少某些不必要的资源消耗，请关注订阅号"余汉波"，发送"资源下载"获取验证码，输入验证码进行下载。

若能访问 github，也可以拉取整个库，或通过夸克网盘下载，这边就不用支付相应的资源流量费。若愿意在程序小店付费下载就更好了，0.99 元。

## 2. python 程序代码的加载

程序中显示的所有 python 程序代码是放在本地文件夹 resources\app\software 中，将需要运行的代码放到该文件夹中便可运行（最好一个 python 程序或代码创建一个文件夹，以免混杂，更好管理），而运行只需双击更可。

加载代码程序的方法有三种：

1. 程序小店的代码程序：双击“腾讯云对象存储下载器”，会出现下面的界面，只需将在程序小店购买获得的链接粘贴到“下载地址”便可。程序就会进行下载并解压文件到 resources\app\software 中，在应用层主界面就能看到该程序。
![](https://gdsx.sanrenjz.com/image/Pasted%20image%2020250608091159.png?imageSlim)

1. github 的代码程序：如果你的代码是在 github 上，那么只需双击"GiHub 仓库下载器"，将仓库地址粘贴上来；选择保存位置，最好是应用的 resources\app\software 文件夹；点击“克隆仓库”便可拉取整个仓库，自动解压到 resources\app\software 中，在应用层主界面就能看到该程序。
![](https://gdsx.sanrenjz.com/image/Pasted%20image%2020250608091625.png?imageSlim)

1. 手动加载：如果你的代码是自己写的，或来自于其他路径，那么可以点击菜单栏的“本地文件”，建议加载整个文件夹，会将整个文件复制到 resources\app\software 文件夹中，容易管理的同时，可以加载相应的说明等，而不是看不懂的文件。
![](https://xz.sanrenjz.com/image/Pasted%20image%2020260531162735.png?imageSlim)

## 3. 程序代码的使用

将程序代码加载进来后，双击便可运行。第一次运行可能会较慢，程序会检查程序代码文件夹的 requirements.txt 文件。若库 requirements.txt 载明的库已经安装会跳过，否则会从 pip ，阿里云镜像或清华镜像中拉取相应的库，进行安装。

若需手动安装相应的库，你可以通过双击“终端模拟器”打开终端，输入 pip 等进行手动安装。

若你的库是自己开发的，或者不是开源库，需要自己将文件放到 resources\python\python-3.12.8-embed-amd64\Lib\site-packages 文件夹内。

# 功能介绍

## 1. 基本功能

* 这是一个基于 Electron 的桌面应用程序，用于管理和运行 Python 脚本，用于提高开发和文件管理效率。
* 支持加密和非加密的 Python 程序
* 提供实时运行日志显示
* 自动管理 Python 依赖
## 2. 版本使用和下载

该程序共提供三个版本，分别命名为：yuhanbopy-xl、yuhanbopy-lh 和 yuhanbopy-mini。其中 yuhanbopy-lh 在 github 的进行开源，地址 [yuhanbo758/yuhanbopy-app: 三人聚智-余汉波程序控制工具](https://github.com/yuhanbo758/yuhanbopy-app)，基于 MIT 许可证发布。

* 夸克网盘：[三人聚智-余汉波程序控制工具](https://pan.quark.cn/s/b13845a1c589)
* 付费下载：[三人聚智-余汉波程序控制工具使用说明 | 三人聚智-余汉波程序小店](https://jy.sanrenjz.com/buy/2)
1. yuhanbopy-xl：有嵌入版 python，无需另外安装 python，适用于电脑小白，下载解压直接使用，效率优先。
1. yuhanbopy-lh：在 yuhanbopy-xl 基础上，植入了 mini QMT 的库 xquant，主要对象是需要小 QMT 量化交易的小白，可以直接加载运行个人提供“通达信与 QMT 结合下单”的 tdx3 程序。
1. yuhanbopy-mini：yuhanbopy-xl 的 mini 版，没有嵌入版 python，安装后首次启动时，系统会要求选择 Python 解释器（.exe 文件）
![](https://gdsx.sanrenjz.com/image/Pasted%20image%2020250917065122.png?imageSlim)

## 3. 程序目录结构

主要程序存放在 app/software 目录下，主要包含三个格式文件，py 或 enc 文件、settings.json 文件和 requirements.txt 文件：

### 3.1 单文件程序

* 支持 .py 文件（普通 Python 文件）
* 支持 .enc 文件（加密的 Python 文件）
### 3.2 文件夹程序

每个程序文件夹可以包含 json 相关说明，示例：

```json
{
    "name": "程序名称",
    "description": "程序描述",
    "main_file": "主程序文件名.py",
    "version": "版本号",
    "author": "作者",
    "category": "分类"
}
```

### 3.3 依赖管理

* 在程序目录中可以放置 requirements.txt 文件
* 系统会自动检查并安装缺失的依赖
* 使用多个 pip 源以提高安装成功率：
* pypi.org
* 清华大学镜像
* 阿里云镜像
## 4. 程序运行

* Windows 64 位操作系统
* 程序列表会显示所有可用的 Python 程序——若文件夹中有 settings.json 文件，显示指定 py 文件，否则显示文件夹中所有 py 文件。
* 双击列表中的程序即可运行
* 运行时会自动打开日志窗口，显示程序输出
* 如果程序有依赖项（requirements.txt 文件），会自动安装所需依赖
* 需加载本地 python 代码，点击右上角“本地文件”，选择 py 文件或文件夹，会将文件或文件夹复制到 app/software 下，创建项目。
![](https://gdsx.sanrenjz.com/image/Pasted%20image%2020250218210349.png?imageSlim)

## 更新说明

本节归纳近期需要在项目中完成的功能改进、发布流程与文档整理要点（已去掉时间戳与细节日期）。主要改动与工作项：

* 代码清理与开源准备：检查并删除无用或测试代码文件，避免影响后续管理与发布；在开源前进行隐私/敏感信息扫描并修复问题（建议使用 security skill 扫描）。
* 文档与说明整理：使用 readme-updater 同步或生成项目级 README；将插件的完整功能介绍与使用说明从 settings.json 中迁移到插件目录下的 README.md（settings.json 的 description 字段仅保留一行简要说明），并在应用界面“详情”中打开该 README。
* 自动更新与发布流程：为应用实现自动升级机制，优先通过站点对象存储拉取更新（示例地址：xz.sanrenjz.com），若对象存储没有对应平台或版本则回退至 GitHub Releases；后续自动上传封装好的安装包到 GitHub Releases；配置 GitHub Actions（可通过 github-auto-package skill）实现每次提交触发自动打包，并按约定的版本号规则递增、产出多平台构建（Windows/macOS/Linux）。
* 发布与资产管理：统一 Release 资产命名为 yuhanbopy-app+<版本号>，排查并移除非必须的发布资产（例如调试用的 builder-debug.yml 等），以免用户困惑。
* UI 与运行体验优化：移除界面中不应展示的提示性/标记性文字；登录头像使用应用 logo（登录用户在 logo 右下显示“会员”角标）；在菜单中增加“设置”与“打开本地插件文件夹”入口，修正“运行 / 详情”按钮的布局，使其位于插件卡片内并对齐。
* 插件管理与运行：下载的插件自动解压到相对路径 app\software（应用自动读取该目录）；在应用内增加“详情”功能以打开插件 README 便于快速上手；优化后台进程管理，确保用户关闭主程序后相关后台任务能够完整退出，修复与磁盘缓存创建相关的错误日志。
建议的执行顺序（便于风险控制）：

1. 先做代码清理并运行隐私/敏感信息扫描；
1. 按需把插件说明迁移到 README 并用 readme-updater 同步；
1. 配置并验证 GitHub Actions 的自动打包流程（多平台与命名规范）；
1. 修复后台进程与缓存相关 bug；
1. 最后做前端 UI 调整与发布资产清理。
## 项目仓库 README 要点

以下内容为仓库 yuhanbopy-app README 的精要摘录，便于在本说明文档中快速参考：

* 项目简介：基于 Electron 的 Windows 桌面应用，用于分发、管理和运行加密保护的 Python 工具（内嵌 Python 3.12 运行时）。核心功能包括一键运行插件（支持 .py、.enc、.zip）、从 GitHub / 腾讯云 COS / 通用 URL 获取插件、AES-256-CBC 加密分发、实时日志、程序卡片列表与双源自动更新（对象存储 + GitHub Releases）。
* 技术栈：Electron、electron-builder、electron-updater、Node.js、内嵌 Python 3.12.8、adm-zip、@electron/remote、xtquant 等。
* 系统要求：Windows x64（64 位）；运行时已内嵌 Python，无需额外安装 Python（针对 yuhanbopy-xl/lh 版本）。
* 快速上手：
1. 从 Releases 页面下载已封装的安装包或便携版；
1. 开发环境：git clone → npm install → npm start；
1. 构建安装包：示例 npm run build-win，产物输出到 dist/。
* 目录结构要点：主程序文件（main.js、index.html、log.html），插件放到 app/software/，内嵌 Python 放在 python/python-3.12.8-embed-amd64/。
* 插件开发要点：每个插件放 app/software/<name>/，必须包含 settings.json（含 name、description、main_file、version、author、category），可放 requirements.txt；入口支持 .py（明文）、.enc（AES-256-CBC）或 .zip（按 main.py → name.py → 第一个 .py 顺序查找）。
* 配置与安全：支持通过环境变量 YUHANBOPY_ENC_KEY 覆盖 .enc 解密密钥；解密后临时文件放系统临时目录并在程序退出后清理；ZIP 解压含路径穿越防护（Zip Slip）；UI 输出用 textContent 避免 XSS。
* 发布与贡献：项目采用 MIT 许可证；通过 GitHub Releases 发布安装包；欢迎 Fork / PR / Issue 提交改进建议。作者信息与联系方式也在仓库 README 中给出。
## 5. 安全特性

* 支持 AES-256-CBC 加密的 Python 程序（.enc 文件）
* 加密程序运行时会自动解密到临时目录
* 程序结束后自动清理临时文件
## 6. 注意事项

* 若是 yuhanbopy-mini 应用，确保 Python 解释器路径正确设置
* 建议在程序目录中提供 requirements.txt 声明依赖
* 加密程序需要使用特定的加密工具进行加密
* 程序运行时保持日志窗口打开可查看实时输出
## 7. 错误处理

* 如果遇到 Python 环境问题，可以通过界面重新选择 Python 解释器，或卸载重装
* 依赖安装失败时，日志窗口会显示详细错误信息
* 程序运行错误会在日志窗口中显示具体原因
这个工具设计得比较完善，特别适合管理和分发 Python 程序，同时通过加密机制保护源代码安全。

## 8. 已集成应用

* 终端模拟器: 内置终端工具，支持命令行操作
* 文件下载器: 通用的文件下载工具，支持多种文件格式
* GitHub 仓库下载器: 便捷的 GitHub 仓库克隆和下载工具
* 腾讯云对象存储下载器: 专用的腾讯云 COS 文件下载工具
* 同花顺板块自动交易系统: 基于同花顺板块的自动交易系统
* 通达信板块自动交易系统 4.0: 基于通达信和国金 QMT 的自动化交易系统
* 问财单策略量化交易系统 2.0: 基于问财自然语言查询的量化交易系统
* 自定义工具集成: 可扩展的工具集成平台
### 8.1 系统工具

### 终端模拟器

* 功能: 简单的终端模拟器，可以执行系统命令
* 使用方法:
* 输入任何系统命令来执行
* 输入 'exit' 或 'quit' 退出程序
* 输入 'clear' 清除屏幕
* 输入 'cd 目录路径' 切换工作目录
### 8.2 下载工具

### 文件下载器

* 功能: 通用的文件下载工具
* 使用方法:
1. 在输入框中粘贴文件下载地址
1. 选择文件保存位置
1. 选择是否自动解压 ZIP 文件
1. 点击下载按钮开始下载
### GitHub 仓库下载器

* 功能: GitHub 仓库克隆工具
* 使用方法:
1. 在输入框中粘贴 GitHub 仓库地址
1. 选择保存位置
1. 选择是否自动解压
1. 点击克隆仓库按钮开始下载
### 腾讯云对象存储下载器

* 功能: 腾讯云对象存储文件下载工具
* 使用方法:
1. 在输入框中粘贴文件下载地址
1. 点击下载按钮开始下载
1. 文件将保存到 app/software/ 目录
1. ZIP 文件会自动解压
### 8.3 量化交易系统

### 同花顺板块自动交易系统

[程序小店 - 小QMT-（加密）QMT与同花顺结合：动态板块监控交易](https://shop.sanrenjz.com/python/%E5%B0%8FQMT-%EF%BC%88%E5%8A%A0%E5%AF%86%EF%BC%89QMT%E4%B8%8E%E5%90%8C%E8%8A%B1%E9%A1%BA%E7%BB%93%E5%90%88%EF%BC%9A%E5%8A%A8%E6%80%81%E6%9D%BF%E5%9D%97%E7%9B%91%E6%8E%A7%E4%BA%A4%E6%98%93)

* 功能: 基于同花顺板块的自动交易系统，支持股票和可转债的自动买卖
* 主要特点:
1. 自动监控同花顺自定义板块变化
1. 根据板块内容自动买入或卖出股票
1. 支持设置交易间隔、单笔金额和总金额
1. 支持多种委托方式和价格调整
1. 实时日志显示交易状态
### 通达信板块自动交易系统 4.0

[程序小店 - 小QMT-（加密）QMT与通达信结合 4.0：监测交易系统，通达信公式自动交易系统](https://shop.sanrenjz.com/python/%E5%B0%8FQMT-%EF%BC%88%E5%8A%A0%E5%AF%86%EF%BC%89QMT%E4%B8%8E%E9%80%9A%E8%BE%BE%E4%BF%A1%E7%BB%93%E5%90%88-4.0%EF%BC%9A%E7%9B%91%E6%B5%8B%E4%BA%A4%E6%98%93%E7%B3%BB%E7%BB%9F%EF%BC%8C%E9%80%9A%E8%BE%BE%E4%BF%A1%E5%85%AC%E5%BC%8F%E8%87%AA%E5%8A%A8%E4%BA%A4%E6%98%93%E7%B3%BB%E7%BB%9F)

* 功能: 基于通达信和国金 QMT 的自动化交易系统
* 主要特点:
1. 支持自定义买入卖出板块监控
1. 灵活的交易参数设置
1. 实时委托和成交反馈
1. 智能资金管理和风控
1. 完整的日志记录系统
### 问财单策略量化交易系统 2.0

[程序小店 - 小QMT-（加密）QMT与问财结合-单策略2.0：自然语言自动化交易系统](https://shop.sanrenjz.com/python/%E5%B0%8FQMT-%EF%BC%88%E5%8A%A0%E5%AF%86%EF%BC%89QMT%E4%B8%8E%E9%97%AE%E8%B4%A2%E7%BB%93%E5%90%88-%E5%8D%95%E7%AD%96%E7%95%A52.0%EF%BC%9A%E8%87%AA%E7%84%B6%E8%AF%AD%E8%A8%80%E8%87%AA%E5%8A%A8%E5%8C%96%E4%BA%A4%E6%98%93%E7%B3%BB%E7%BB%9F)

* 功能: 基于问财自然语言查询的量化交易系统
* 主要特点:
1. 支持通过自然语言查询选股
1. 自动执行交易策略
1. 实时查看持仓和资产信息
1. 定时执行策略
1. 支持股票、基金、可转债等多种证券类型
## 9. 插件开发指南

本章节将指导您如何为三人聚智-Python 程序管理工具开发自定义插件。

### 9.1 插件系统概述

插件系统基于标准的目录结构和配置文件，支持以下特性：

* 自动插件发现和加载
* 标准化的配置管理
* 依赖包自动安装
* 统一的界面风格
* 日志和错误处理
### 9.2 插件目录结构

每个插件都应该放在 resources/app/software/ 目录下的独立文件夹中：

```plain text
software/
├── your_plugin_name/
│   ├── settings.json          # 插件配置文件（必需）
│   ├── your_plugin.py         # 主程序文件
│   ├── logo.ico              # 插件图标文件（可选）
│   ├── requirements.txt       # 依赖包列表（可选）
│   ├── plugin_config.json     # 插件运行时配置（可选）
│   └── other_files...         # 其他资源文件
```

### 9.3 配置文件说明

### settings.json（必需）

这是插件的元数据配置文件，系统通过此文件识别和加载插件：

```json
{
    "name": "插件显示名称",
    "description": "插件功能描述\n\n支持多行描述\n可以包含使用说明",
    "main_file": "main_program.py",
    "version": "1.0.0",
    "author": "开发者姓名",
    "category": "插件分类"
}
```

字段说明：

* name: 在界面中显示的插件名称
* description: 插件的详细描述，支持换行符
* main_file: 主程序文件名（相对于插件目录）
* version: 插件版本号
* author: 开发者信息
* category: 插件分类（如：下载工具、量化交易、系统工具等）
### requirements.txt（可选）

列出插件需要的 Python 包依赖：

```plain text
# 插件依赖包列表
requests>=2.25.0
pandas>=1.3.0
numpy>=1.21.0
```

系统会在运行插件前自动安装这些依赖包。

### logo.ico（可选）

插件的自定义图标文件：

* 文件名: 必须命名为 logo.ico
* 格式: ICO 格式图标文件
* 尺寸: 建议使用 32x32 或 48x48 像素
* 位置: 放在插件根目录下
* 作用: 在主界面程序列表中显示为插件图标
图标设计建议：

* 使用简洁明了的设计，便于识别
* 选择与插件功能相关的图形元素
* 确保在小尺寸下仍然清晰可见
* 使用适当的颜色对比度
图标制作方法：

1. 在线工具: 使用 favicon.io、convertio.co 等在线转换工具
1. 图像编辑软件: 使用 Photoshop、GIMP 等软件导出为 ICO 格式
1. 命令行工具: 使用 ImageMagick 等工具进行格式转换
示例转换命令（ImageMagick）：

```bash
# 将PNG图片转换为ICO格式
magick convert logo.png -resize 32x32 logo.ico
```

图标文件要求：

* 文件大小建议不超过 50KB
* 支持透明背景
* 建议包含多个尺寸（16x16, 32x32, 48x48）
如果不提供 logo.ico 文件，系统将使用默认图标显示插件。插件模板目录中包含了一个示例图标文件供参考。

### 9.4 插件开发规范

### 9.4.1 基本结构

插件主程序应该遵循以下基本结构：

```python
# -*- coding: utf-8 -*-
"""
插件名称
作者: 开发者姓名
版本: 1.0.0
描述: 插件功能描述
"""

import tkinter as tk
from tkinter import ttk, messagebox
import json
import os

class YourPlugin:
    """插件主类"""
    
    def __init__(self, root):
        """初始化插件"""
        self.root = root
        self.root.title("插件名称")
        self.root.geometry("800x600")
        
        # 加载配置
        self.config = self.load_config()
        
        # 创建界面
        self.create_widgets()
    
    def load_config(self):
        """加载插件配置"""
        # 配置文件加载逻辑
        pass
    
    def create_widgets(self):
        """创建界面组件"""
        # 界面创建逻辑
        pass

def main():
    """主函数 - 插件入口点"""
    try:
        root = tk.Tk()
        app = YourPlugin(root)
        root.mainloop()
    except Exception as e:
        print(f"插件运行出错: {e}")
        messagebox.showerror("错误", f"插件运行出错: {e}")

if __name__ == "__main__":
    main()
```

### 9.4.2 界面设计建议

1. 使用 Tkinter: 推荐使用 Tkinter 作为 GUI 框架，确保兼容性
1. 响应式布局: 使用 grid 或 pack 布局管理器创建响应式界面
1. 统一风格: 使用 ttk 组件保持界面风格一致
1. 错误处理: 添加适当的异常处理和用户提示
### 9.4.3 配置管理

插件应该支持配置文件管理：

```python
def load_config(self):
    """加载配置文件"""
    config_path = "plugin_config.json"
    default_config = {
        "setting1": "default_value1",
        "setting2": "default_value2"
    }
    
    try:
        if os.path.exists(config_path):
            with open(config_path, 'r', encoding='utf-8') as f:
                config = json.load(f)
            # 合并默认配置
            for key, value in default_config.items():
                if key not in config:
                    config[key] = value
            return config
        else:
            self.save_config(default_config)
            return default_config
    except Exception as e:
        messagebox.showerror("错误", f"加载配置失败: {e}")
        return default_config

def save_config(self, config=None):
    """保存配置文件"""
    if config is None:
        config = self.config
    
    try:
        with open("plugin_config.json", 'w', encoding='utf-8') as f:
            json.dump(config, f, ensure_ascii=False, indent=4)
    except Exception as e:
        messagebox.showerror("错误", f"保存配置失败: {e}")
```

### 9.5 插件开发模板

系统提供了一个完整的插件开发模板，位于：
resources/app/software/plugin_template/

该模板包含：

* 完整的插件结构示例
* 标准的配置文件管理
* 界面组件创建示例
* 错误处理机制
* 日志输出功能
您可以复制此模板作为新插件的起点。

### 9.6 插件测试和调试

### 9.6.1 本地测试

1. 将插件文件夹放入 resources/app/software/ 目录
1. 重启应用程序
1. 在主界面中找到您的插件并运行
### 9.6.2 调试技巧

1. 控制台输出: 使用 print() 输出调试信息
1. 日志记录: 在界面中添加日志输出区域
1. 异常处理: 使用 try-catch 捕获和显示错误
1. 配置验证: 确保配置文件格式正确
### 9.7 插件发布和分享

### 9.7.1 打包插件

1. 确保所有必要文件都在插件目录中
1. 测试插件在不同环境下的运行情况
1. 编写详细的使用说明
### 9.7.2 分享插件

* 可以将插件目录打包为 ZIP 文件分享
* 其他用户只需解压到 software/ 目录即可使用
* 建议在 GitHub 等平台分享插件代码
### 9.8 常见问题和解决方案

### Q: 插件无法在主界面显示？

A: 检查 settings.json 文件格式是否正确，确保 main_file 字段指向正确的文件。

### Q: 依赖包安装失败？

A: 检查 requirements.txt 文件格式，确保包名和版本号正确。

### Q: 插件运行时出现编码错误？

A: 确保所有 Python 文件都使用 UTF-8 编码，并在文件开头添加编码声明。

### Q: 如何访问插件的工作目录？

A: 插件运行时的工作目录就是插件所在的文件夹，可以直接使用相对路径访问资源文件。

### Q: 插件图标不显示或显示为默认图标？

A: 检查以下几点：

1. 确保图标文件命名为 logo.ico（区分大小写）
1. 确保图标文件格式为标准的 ICO 格式
1. 重启应用程序以刷新图标缓存
1. 检查图标文件是否损坏，可以尝试重新制作
### Q: 如何制作高质量的插件图标？

A: 建议步骤：

1. 设计 48x48 像素的原始图标
1. 确保图标在小尺寸下仍然清晰
1. 使用在线工具或专业软件转换为 ICO 格式
1. 测试图标在不同背景下的显示效果
### 9.9 高级功能

### 9.9.1 加密插件

系统支持加密的 .enc 文件，可以保护插件源代码。

### 9.9.2 多文件插件

插件可以包含多个 Python 文件，通过 import 语句相互调用。

### 9.9.3 资源文件管理

插件可以包含图片、数据文件等资源，放在插件目录中即可访问。

常见资源文件类型：

* logo.ico: 插件图标文件，用于在主界面显示
* 数据文件: CSV、JSON、XML 等数据文件
* 配置模板: 默认配置文件模板
* 帮助文档: README、使用说明等文档
* 其他图片: PNG、JPG 等图片资源
资源文件访问示例：

```python
import os
from pathlib import Path

# 获取插件目录路径
plugin_dir = Path(__file__).parent

# 访问资源文件
icon_path = plugin_dir / "logo.ico"
data_path = plugin_dir / "data" / "sample.csv"
config_template = plugin_dir / "default_config.json"

# 检查文件是否存在
if icon_path.exists():
    print(f"图标文件存在: {icon_path}")
```

## 10. 插件集成和配置详解

### 10.1 插件自动发现机制

系统启动时会自动扫描 resources/app/software/ 目录下的所有子目录和文件：

1. 目录扫描: 系统会遍历 software 目录下的所有子文件夹
1. 配置检测: 检查每个文件夹中是否存在 settings.json 文件
1. 插件注册: 根据配置文件信息将插件注册到系统中
1. 界面显示: 在主界面的程序列表中显示可用插件
### 10.2 插件加载流程

当用户点击运行插件时，系统执行以下步骤：

```plain text
1. 读取插件配置 (settings.json)
2. 检查依赖包 (requirements.txt)
3. 安装缺失的依赖包
4. 创建独立的Python进程
5. 设置工作目录为插件目录
6. 执行主程序文件
7. 监控进程状态和输出
```

### 10.3 依赖包管理

### 10.3.1 自动安装机制

系统会在运行插件前自动检查和安装依赖包：

```python
# requirements.txt 示例
requests>=2.25.0          # 指定最低版本
pandas==1.3.5             # 指定确切版本
numpy                      # 使用最新版本
matplotlib>=3.0.0,<4.0.0  # 版本范围限制
```

### 10.3.2 依赖包安装位置

* 依赖包安装在系统的 Python 环境中
* 所有插件共享相同的依赖包环境
* 建议使用兼容的包版本避免冲突
### 10.3.3 常用依赖包推荐

```plain text
# 界面开发
tkinter                    # 内置GUI库（推荐）
pillow>=8.0.0             # 图像处理

# 数据处理
pandas>=1.3.0             # 数据分析
numpy>=1.21.0             # 数值计算
openpyxl>=3.0.0           # Excel文件处理

# 网络请求
requests>=2.25.0          # HTTP请求
urllib3>=1.26.0           # URL处理

# 文件处理
pathlib                   # 路径处理（内置）
json                      # JSON处理（内置）
configparser              # 配置文件处理（内置）
```

### 10.4 插件配置管理最佳实践

### 10.4.1 配置文件结构

建议使用分层的配置文件结构：

```plain text
plugin_directory/
├── settings.json          # 插件元数据（系统读取）
├── config.json           # 用户配置（插件读取）
├── default_config.json   # 默认配置模板
└── user_data/            # 用户数据目录
    ├── logs/             # 日志文件
    ├── cache/            # 缓存文件
    └── exports/          # 导出文件
```

### 10.4.2 配置文件示例

settings.json（系统配置）:

```json
{
    "name": "数据分析工具",
    "description": "强大的数据分析和可视化工具\n\n功能特性：\n- 支持多种数据格式\n- 实时图表生成\n- 数据导出功能",
    "main_file": "data_analyzer.py",
    "version": "2.1.0",
    "author": "开发者姓名",
    "category": "数据工具",
    "icon": "icon.png",
    "min_python_version": "3.7",
    "supported_os": ["windows", "linux", "macos"]
}
```

config.json（用户配置）:

```json
{
    "ui_settings": {
        "theme": "light",
        "window_size": "800x600",
        "auto_save": true
    },
    "data_settings": {
        "default_format": "xlsx",
        "max_rows": 10000,
        "encoding": "utf-8"
    },
    "export_settings": {
        "default_path": "./exports/",
        "include_timestamp": true,
        "compression": false
    }
}
```

### 10.4.3 配置管理代码示例

```python
import json
import os
from pathlib import Path

class ConfigManager:
    """配置管理器"""
    
    def __init__(self, plugin_dir=None):
        """初始化配置管理器"""
        self.plugin_dir = Path(plugin_dir) if plugin_dir else Path.cwd()
        self.config_file = self.plugin_dir / "config.json"
        self.default_config_file = self.plugin_dir / "default_config.json"
        
    def load_config(self):
        """加载配置文件"""
        # 加载默认配置
        default_config = self.load_default_config()
        
        # 加载用户配置
        if self.config_file.exists():
            try:
                with open(self.config_file, 'r', encoding='utf-8') as f:
                    user_config = json.load(f)
                # 合并配置
                config = self.merge_config(default_config, user_config)
            except Exception as e:
                print(f"加载用户配置失败: {e}")
                config = default_config
        else:
            config = default_config
            self.save_config(config)
        
        return config
    
    def load_default_config(self):
        """加载默认配置"""
        if self.default_config_file.exists():
            try:
                with open(self.default_config_file, 'r', encoding='utf-8') as f:
                    return json.load(f)
            except Exception as e:
                print(f"加载默认配置失败: {e}")
        
        # 返回硬编码的默认配置
        return {
            "ui_settings": {
                "theme": "light",
                "window_size": "800x600"
            },
            "data_settings": {
                "default_format": "xlsx",
                "max_rows": 10000
            }
        }
    
    def save_config(self, config):
        """保存配置文件"""
        try:
            with open(self.config_file, 'w', encoding='utf-8') as f:
                json.dump(config, f, ensure_ascii=False, indent=4)
        except Exception as e:
            print(f"保存配置失败: {e}")
    
    def merge_config(self, default, user):
        """合并配置"""
        result = default.copy()
        for key, value in user.items():
            if key in result and isinstance(result[key], dict) and isinstance(value, dict):
                result[key] = self.merge_config(result[key], value)
            else:
                result[key] = value
        return result
```

### 10.5 插件生命周期管理

### 10.5.1 插件状态

系统跟踪每个插件的运行状态：

* 未运行: 插件已加载但未启动
* 运行中: 插件正在执行
* 已停止: 插件执行完成或被用户停止
* 错误: 插件运行时发生错误
### 10.5.2 进程管理

```javascript
// 软件管理器中的进程管理（参考）
class SoftwareManager {
    constructor() {
        this.runningProcesses = new Map(); // 存储运行中的进程
    }
    
    // 启动插件
    async runSoftware(softwarePath, softwareName) {
        // 创建Python进程
        // 设置工作目录
        // 监控输出和错误
        // 注册进程到管理器
    }
    
    // 停止插件
    stopSoftware(softwareName) {
        // 查找进程
        // 发送终止信号
        // 清理资源
    }
}
```

### 10.6 插件调试和日志

### 10.6.1 日志记录最佳实践

```python
import logging
import os
from datetime import datetime

class PluginLogger:
    """插件日志管理器"""
    
    def __init__(self, plugin_name, log_dir="logs"):
        """初始化日志器"""
        self.plugin_name = plugin_name
        self.log_dir = log_dir
        
        # 创建日志目录
        os.makedirs(log_dir, exist_ok=True)
        
        # 配置日志器
        self.logger = logging.getLogger(plugin_name)
        self.logger.setLevel(logging.DEBUG)
        
        # 创建文件处理器
        log_file = os.path.join(log_dir, f"{plugin_name}_{datetime.now().strftime('%Y%m%d')}.log")
        file_handler = logging.FileHandler(log_file, encoding='utf-8')
        file_handler.setLevel(logging.DEBUG)
        
        # 创建控制台处理器
        console_handler = logging.StreamHandler()
        console_handler.setLevel(logging.INFO)
        
        # 设置格式
        formatter = logging.Formatter(
            '%(asctime)s - %(name)s - %(levelname)s - %(message)s'
        )
        file_handler.setFormatter(formatter)
        console_handler.setFormatter(formatter)
        
        # 添加处理器
        self.logger.addHandler(file_handler)
        self.logger.addHandler(console_handler)
    
    def info(self, message):
        """记录信息日志"""
        self.logger.info(message)
    
    def error(self, message):
        """记录错误日志"""
        self.logger.error(message)
    
    def debug(self, message):
        """记录调试日志"""
        self.logger.debug(message)
```

### 10.6.2 错误处理和用户反馈

```python
def safe_execute(func, error_message="操作失败"):
    """安全执行函数，捕获异常并显示用户友好的错误信息"""
    try:
        return func()
    except FileNotFoundError as e:
        messagebox.showerror("文件错误", f"找不到文件: {e}")
        logger.error(f"文件未找到: {e}")
    except PermissionError as e:
        messagebox.showerror("权限错误", f"没有访问权限: {e}")
        logger.error(f"权限错误: {e}")
    except json.JSONDecodeError as e:
        messagebox.showerror("配置错误", f"配置文件格式错误: {e}")
        logger.error(f"JSON解析错误: {e}")
    except Exception as e:
        messagebox.showerror("错误", f"{error_message}: {e}")
        logger.error(f"未知错误: {e}")
    return None
```

### 10.7 插件性能优化

### 10.7.1 启动优化

* 延迟加载非必需模块
* 使用配置缓存
* 优化界面初始化
### 10.7.2 内存管理

* 及时释放大对象
* 使用生成器处理大数据
* 避免内存泄漏
### 10.7.3 响应性优化

```python
import threading
from tkinter import ttk

class ResponsivePlugin:
    """响应式插件示例"""
    
    def __init__(self, root):
        self.root = root
        self.progress_var = tk.StringVar()
        self.create_widgets()
    
    def create_widgets(self):
        """创建界面"""
        # 进度条
        self.progress = ttk.Progressbar(
            self.root, 
            mode='indeterminate'
        )
        self.progress.pack(pady=10)
        
        # 状态标签
        self.status_label = ttk.Label(
            self.root, 
            textvariable=self.progress_var
        )
        self.status_label.pack()
    
    def long_running_task(self):
        """长时间运行的任务"""
        def task():
            self.progress.start()
            self.progress_var.set("正在处理...")
            
            try:
                # 执行耗时操作
                self.do_heavy_work()
                self.progress_var.set("完成")
            except Exception as e:
                self.progress_var.set(f"错误: {e}")
            finally:
                self.progress.stop()
        
        # 在后台线程中执行
        threading.Thread(target=task, daemon=True).start()
```

### 10.8 插件安全考虑

### 10.8.1 文件访问安全

* 限制文件访问范围
* 验证文件路径
* 避免执行外部命令
### 10.8.2 网络安全

* 验证 URL 和证书
* 处理网络超时
* 保护敏感信息
### 10.8.3 用户输入验证

```python
def validate_input(value, input_type="string", max_length=None, allowed_chars=None):
    """输入验证函数"""
    if input_type == "string":
        if max_length and len(value) > max_length:
            raise ValueError(f"输入长度不能超过{max_length}字符")
        if allowed_chars and not all(c in allowed_chars for c in value):
            raise ValueError("包含非法字符")
    elif input_type == "number":
        try:
            float(value)
        except ValueError:
            raise ValueError("必须输入数字")
    
    return True
```

---

其他应用程序正创建中，可关注右上方"程序小店"，获取更多可视化 python 应用程序。

* GitHub Issues: [https://github.com/yuhanbo758/yuhanbopy-app/issues](https://github.com/yuhanbo758/yuhanbopy-app/issues)
## 11.版权信息

版权所有 © 2025 余汉波
基于 MIT 许可证发布

![](https://gdsx.sanrenjz.com/image/sanrenjz_yuhanbolh_yuhanbo758.png?imageSlim&t=1ab9b82c-e220-8022-beff-e265a194292a)

