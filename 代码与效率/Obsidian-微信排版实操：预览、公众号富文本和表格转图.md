程序小店：[程序小店 - obsidian插件-yuhanbo-wechat-public](https://shop.sanrenjz.com/obsidian/obsidian%E6%8F%92%E4%BB%B6-yuhanbo-wechat-public)

bili 视频：[Obsidian 微信排版实操：预览、公众号富文本和表格转图_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1R4yzzAEDn/?vd_source=247ac77d4ae7339ea06d0fec09aa8f70)

* [Obsidian 社区插件安装](https://community.obsidian.md/plugins/yuhanbo-wechat-public)
* [安装包下载（GitHub Releases）](https://github.com/yuhanbo758/obsidian-yuhanbo-wechat-public/releases/latest)
* [安装与使用文档](https://github.com/yuhanbo758/obsidian-yuhanbo-wechat-public#usage)
在 Obsidian 写好稿件后，先在右侧调出公众号排版，再按粘贴目标选复制方式。yuhanbo-wechat-public 的排版预览和普通复制免费。需要把微信样式带到公众号后台，或者需要把表格做成 PNG，可以用授权码开启「微信复制」和「图表复制」。

![](https://xz.sanrenjz.com/image/%E8%A7%86%E9%A2%91%E5%B0%81%E9%9D%A2_16%E6%AF%949_Obsidian%20%E5%BE%AE%E4%BF%A1%E6%8E%92%E7%89%88.png?imageSlim)

## 先在同一篇笔记里看排版

打开一篇 Markdown 笔记。在 Windows 按 Ctrl+P 打开 Obsidian 命令面板，搜索并执行「打开微信Markdown编辑器」。右侧出现预览，左侧可以继续编辑原稿。侧边工具栏的编辑图标也能打开该窗口。

可以用下面这种有标题和表格的内容试一遍。演示还在笔记末尾放了 Mermaid 流程图和代码块，用来检查复杂正文能否正确预览。

```markdown
# 周末城市漫步

下面是三站路线与建议用时。

| 站点 | 活动 | 建议用时 |
| --- | --- | ---: |
| 河岸步道 | 看江景、拍照 | 30 分钟 |
| 城市书屋 | 阅读、休息 | 40 分钟 |
| 社区公园 | 野餐、散步 | 50 分钟 |
```

![](https://xz.sanrenjz.com/image/%E5%AE%9E%E5%BD%95%E6%88%AA%E5%9B%BE-%E7%AC%94%E8%AE%B0%E4%B8%8E%E5%8F%B3%E4%BE%A7%E9%A2%84%E8%A7%88.png?imageSlim)

右侧工具栏可切换经典、优雅、简洁三套主题，再调整主题色、字体和字号。演示用同一篇笔记切换到优雅主题、玫瑰金和 18px，方便对照内容相同、样式变化的效果。

## 决定何时同步预览

在「设置 → yuhanbo-wechat-public」找到「自动同步」。开启时，只有插件侧栏实际可见才会随笔记更新。切到日历等其他侧栏或把侧栏折叠时，后台预览暂停。视频实测了折叠期间编辑、重新展开后显示最新内容的过程。关闭自动同步后，编辑新内容，再点工具栏「刷新」。

插件设置还提供字体、字号、代码块主题和自定义 CSS。默认值包括经典主题、经典蓝、无衬线、16px、GitHub 代码块主题及开启自动同步。底部可看到「自动保存」和「导出格式」控件。演示只展示这些控件的位置；命令「导出当前文档为微信格式」实际走微信复制流程，需要相应授权。

工具栏的「相对路径」已实测能复制笔记在库内的路径。本次测试中，「绝对路径」复制出的地址没有指向实际文件，演示采用「相对路径」。

## 同一篇笔记试三种复制

| 模式 | 授权 | 适合做什么 |
| --- | --- | --- |
| 普通复制 | 免费 | 保留富文本和可编辑的 HTML 表格，适合继续修改内容 |
| 微信复制 | 需要授权 | 将公众号排版样式写进富文本，粘到微信公众号后台后再预览发布 |
| 图表复制 | 需要授权 | 将 Markdown 文字表格变为嵌入正文的 PNG，正文继续保留富文本 |视频打开本地粘贴对照窗口，展示三次从插件实际复制的剪贴板内容。普通复制结果仍有 HTML 表格；微信复制结果可检查排版样式；图表复制后，同一张表成为 PNG。图片里的数值要回到原笔记修改，再重新复制。

![](https://xz.sanrenjz.com/image/%E5%AE%9E%E5%BD%95%E6%88%AA%E5%9B%BE-%E8%A1%A8%E6%A0%BC%E5%B7%B2%E8%BD%AC%E4%B8%BAPNG.png?imageSlim)

## 购买并激活两项付费复制

1. 打开「设置 → yuhanbo-wechat-public → 复制功能授权」。「前往程序小店购买授权码」在演示所用构建中已接入。也可以直接打开[程序小店商品页](https://shop.sanrenjz.com/obsidian/obsidian%E6%8F%92%E4%BB%B6-yuhanbo-wechat-public)。
1. 将收到的授权码粘贴到「授权码」输入框，然后点「激活」。已有授权码可直接粘贴。当前演示授权同时包含「微信复制」和「图表复制」。
1. 确认状态显示已授权，再回到右侧预览选择需要的按钮。授权在本地验证。录制使用作者提供的演示授权，画面不公开授权码，购买和发码流程由店铺处理。
## 从哪里安装

在桌面版 Obsidian 打开「设置 → 第三方插件 → 浏览」，搜索准确名称 yuhanbo-wechat-public，打开详情后安装并启用。可先查看[Obsidian 官方社区条目](https://community.obsidian.md/plugins/yuhanbo-wechat-public)。

需要手动安装时，从 [GitHub 正式发行页](https://github.com/yuhanbo758/obsidian-yuhanbo-wechat-public/releases/latest) 下载同一版本的 main.js、manifest.json、styles.css，放进库配置目录的 plugins/yuhanbo-wechat-public/，再回到 Obsidian 启用。旧测试版插件 ID 与社区版不同，先确认启用的是目标版本。

本教程在 Windows 版 Obsidian 1.15.1 的测试库录制。演示版本为 1.1.5 的本地构建，包含后来加到设置页中的购买入口。社区发行版是否已有该入口，以实际安装的版本为准。公众号后台最终版式以粘贴后的预览为准。

![](https://xz.sanrenjz.com/image/%E6%B5%81%E7%A8%8B%E5%9B%BE-%E6%93%8D%E4%BD%9C%E6%B5%81%E7%A8%8B%E5%9B%9E%E9%A1%BE.png?imageSlim)

