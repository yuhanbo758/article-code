写项目周报时，可以用 yuhanbo-editing 切标题、引用已有笔记、给重点内容加粗或高亮，再把表格搬进正文。遇到混用的中文标点和繁体字，也能在编辑器中直接转换。下文用一个独立演示库走一遍这些操作。

bili 视频：[Obsidian 编辑提速：标题、双链、表格和中文整理_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1rPyGzPEBh/?vd_source=247ac77d4ae7339ea06d0fec09aa8f70)

程序小店：[程序小店 - obsidian插件-yuhanbo-editing 编辑增强](https://shop.sanrenjz.com/obsidian/obsidian%E6%8F%92%E4%BB%B6-yuhanbo-editing-%E7%BC%96%E8%BE%91%E5%A2%9E%E5%BC%BA)

* [安装与使用文档](https://github.com/yuhanbo758/obsidian-yuhanb-editing)
* [安装文件下载（GitHub Releases）](https://github.com/yuhanbo758/obsidian-yuhanb-editing/releases/latest)
![](https://xz.sanrenjz.com/image/%E8%A7%86%E9%A2%91%E5%B0%81%E9%9D%A2_16%E6%AF%949_112.png?imageSlim)

## 从哪里安装和打开

本教程使用 yuhanbo-editing 1.1.6，需要 Obsidian 桌面版 1.14.4 或更高版本。视频在 Windows 上使用 Obsidian 1.15.1 实录。

1. 在 Obsidian 打开「设置 → 第三方插件 → 浏览」，搜索 yuhanbo-editing。
1. 打开插件详情，点击「安装」，安装完成后点击「启用」。已安装的版本会在详情显示「已安装」。本机在 Obsidian 1.15.1 的社区市场实测可搜索到 1.1.6。
1. 回到 Markdown 编辑器，按 Ctrl+P（macOS 是 Cmd+P）打开命令面板，输入 yuhanbo-editing。可执行具体命令，也可以打开「编辑工具菜单」。
![](https://xz.sanrenjz.com/image/%E5%AE%9E%E5%BD%95%E6%88%AA%E5%9B%BE-%E6%8F%92%E4%BB%B6%E5%85%A5%E5%8F%A3.png?imageSlim)

在「已安装插件」里打开插件右侧更多菜单中的「设置」，即可查看标题快捷键和自动表格转换。 [Obsidian 社区插件帮助](https://obsidian.md/help/community-plugins)

备用安装　如果当前无法访问社区市场，从 [GitHub Releases](https://github.com/yuhanbo758/obsidian-yuhanb-editing/releases/latest) 下载 main.js、manifest.json 和 styles.css。把三个文件放到库根目录的 .obsidian/plugins/yuhanbo-editing/，重载插件列表后启用。

## 一、给「项目周报」设标题

新建一篇笔记，在正文第一行输入「项目周报」。把光标放在这一行，按 Ctrl+2，当前行变成二级标题。再按一次同一个组合键，行首的标题标记会取消。Windows 和 Linux 用 Ctrl+1～6，macOS 用 Cmd+1～6。选中多行时可以批量改标题。

如果按键仍在切换标签页，先确认焦点在 Markdown 正文，再到插件设置核对「编辑器内优先使用标题快捷键」。你在 Obsidian 中手动设置的快捷键会优先处理。

## 二、把已有笔记名批量转成双链

在同一个库里新建「发布清单」和「复盘记录」两篇笔记，在周报里输入「这一周先看发布清单和复盘记录。」选中这一行，执行 将已知笔记名批量转换为内链。源码模式会显示以下结果：

```markdown
这一周先看[[发布清单]]和[[复盘记录]]。
```

这个命令匹配库里已经存在的 Markdown 笔记名。切到阅读视图，点击「发布清单」即可打开对应笔记。

## 三、给 Markdown 正文加粗或高亮

选中要强调的文字，在 打开编辑工具菜单 里选择 切换粗体。源码模式显示 **文字**。再从命令面板执行 切换高亮，就能在阅读视图里看到高亮样式。对同一选区再次执行相应命令可取消格式。

本次 Windows 实测里，Alt+G 被另一个应用的全局快捷键拦截。通过 Obsidian 的命令面板仍可成功执行 切换高亮。

## 四、统一中文标点，把繁体转成简体

* 选中 项目说明,还可以调整中文标点!，执行 英文标点转中文，得到「项目说明，还可以调整中文标点！」。
* 选中 這是繁體字，請確認專案資訊。，执行 繁体转简体，得到「这是繁体字，请确认专案资讯。」。
## 五、复制表格，在周报里生成 Markdown 表格

1. 复制一小块带表头的数据，例如「任务、状态、安排」三列。可以从表格软件复制，也可像视频一样从文本文件复制以制表符分列的示例数据。
1. 在周报正文把光标放到「进度表」下方空行，执行 智能粘贴表格。Windows 演示使用 Ctrl+Alt+V，也可从命令面板执行。
1. 第一行会成为表头。先在源码模式检查 Markdown，再切到阅读视图核对排版。
![](https://xz.sanrenjz.com/image/%E5%AE%9E%E5%BD%95%E6%88%AA%E5%9B%BE-%E7%94%9F%E6%88%90%E8%A1%A8%E6%A0%BC.png?imageSlim)

## 六、常用表格时，用普通粘贴自动转换

1. 在插件设置开启 自动将粘贴表格转为 Markdown。
1. 复制有表头的制表符数据。回到笔记空行，直接按 Ctrl+V（macOS 是 Cmd+V）。
1. 实测「下周计划」里生成了「任务、负责人、截止」三列表格，可切到阅读视图核对。
这个选项默认关闭。偶尔处理表格时，可以继续用「智能粘贴表格」命令；想让粘贴自动识别表格，再开启这项设置。普通 Markdown 表格无法表达合并单元格，插件会保留左上角文本并用空单元格占位。

## 操作回顾

启用插件 → 切换标题 → 转换双链 → 加粗或高亮 → 整理中文标点和简繁 → 智能粘贴表格。

![](https://xz.sanrenjz.com/image/%E6%B5%81%E7%A8%8B%E5%9B%BE-%E6%93%8D%E4%BD%9C%E5%9B%9E%E9%A1%BE.png?imageSlim)

项目入口 [GitHub 源码与中文说明](https://github.com/yuhanbo758/obsidian-yuhanb-editing) · [版本与安装文件](https://github.com/yuhanbo758/obsidian-yuhanb-editing/releases/latest)

