[OB插件yuhanbo-python：在笔记中直接运行 Python 代码，提升学习工作效率！_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV18wiBYXEnz/?vd_source=247ac77d4ae7339ea06d0fec09aa8f70#reply113605743805025)

## 简介

Obsidian Python Runner 是一个允许您在 Obsidian 笔记中直接运行 Python 代码的插件。它提供了一个简单的界面来执行 Python 代码并查看输出结果。

## 功能特点

* 在 Obsidian 笔记中直接运行 Python 代码
* 可拖动的输出窗口
* 支持复制执行结果
* 可自定义 Python 解释器路径
## 安装要求

* Obsidian 版本 >= 0.15.0
* 系统中已安装 Python
![](https://image.sanrenjz.com/Pasted%20image%2020241206115455.png)

## 使用方法

### 1. 编写 Python 代码

在 Obsidian 笔记中，使用 Python 代码块来编写代码：

    ```python

    print("Hello, World!")

    ```

### 2. 运行代码

* 在代码块下方会出现一个"运行"按钮
* 点击按钮执行代码
* 执行结果会在弹出窗口中显示
### 3. 查看结果

* 执行结果会在一个可拖动的模态窗口中显示
* 可以使用窗口顶部的"复制"按钮复制输出内容
* 点击关闭按钮或窗口外部区域可关闭结果窗口
## 插件设置

### Python 路径配置

1. 进入 Obsidian 设置
1. 找到"Python Runner"插件设置
1. 在"Python 路径"输入框中设置 Python 解释器的路径
   - Windows 默认值: python

   - 如果 Python 未在环境变量中，需要输入完整路径，如：C:\Python39\python.exe

## 注意事项

* 代码执行超时时间为 30 秒
* 临时文件会在代码执行后自动清理
* 确保系统编码设置正确，以支持中文输出
* 建议使用 Python 3.x 版本
## 常见问题

### 1. Python 路径设置问题

如果遇到"找不到 Python"的错误，请检查：

* Python 是否正确安装
* 环境变量是否正确设置
* 插件设置中的 Python 路径是否正确
### 2. 中文显示问题

如果输出中文显示乱码：

* 确保系统使用 UTF-8 编码
* Windows 用户可能需要在命令行中执行 chcp 65001
### 3. 执行超时

* 如果代码执行时间过长，将在 30 秒后自动终止
* 请优化代码执行效率或分段执行
## 技术支持

如果遇到问题，请：

1. 检查 Python 安装和环境变量设置
1. 查看控制台错误日志
1. 提交 issue 到项目仓库
## 下载链接：[obsidian-yuhanbo-python](https://kdy.sanrenjz.com/#s/_EANZqEQ)

下载资源存放于自建站的对象存储中，规避爬虫等不必要的流量，需关注微信公众号获得提取码：余汉波-发送“资源下载”。

受限于流量资费昂贵，早期可能不会提供大资源，需跳转到官网或第三方网盘下载。

![](https://gdsx.sanrenjz.com/PicGo/%E5%85%A8%E7%A0%81%E5%90%88%E4%B8%80.png)

