开会时，把议程和记录并排打开。写稿时，再换成提纲和参考资料。yuhanbo-workspaces 可以把这两组标签页分别保存为「会议桌」和「写作台」，下次直接从切换器加载整套布局。收藏的工作区会排在列表顶部，也可以在修改前复制布局或备份配置。

程序小店：[程序小店 - obsidian插件-yuhanbo-workspaces，工作区管理](https://shop.sanrenjz.com/obsidian/obsidian%E6%8F%92%E4%BB%B6-yuhanbo-workspaces%EF%BC%8C%E5%B7%A5%E4%BD%9C%E5%8C%BA%E7%AE%A1%E7%90%86)
bili 视频：[Obsidian 工作区管理：保存、切换与备份布局_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1tG1MzKE6g/?vd_source=247ac77d4ae7339ea06d0fec09aa8f70)

* [Obsidian 社区插件目录](https://community.obsidian.md/plugins/yuhanbo-workspaces)
* [安装文件下载](https://github.com/yuhanbo758/obsidian-yuhanbo-workspaces/releases/tag/0.9.7)
![](https://xz.sanrenjz.com/image/%E8%A7%86%E9%A2%91%E5%B0%81%E9%9D%A2_16%E6%AF%949_Obsidian%20%E5%B7%A5%E4%BD%9C%E5%8C%BA%E7%AE%A1%E7%90%86.png?imageSlim)

本教程演示 Obsidian 1.15.1 桌面端和 yuhanbo-workspaces 0.9.7，使用四份虚构笔记。[社区目录](https://community.obsidian.md/plugins/yuhanbo-workspaces) · [版本与安装文件](https://github.com/yuhanbo758/obsidian-yuhanbo-workspaces/releases/tag/0.9.7)

## 安装并找到命令

1. 在 Obsidian 设置 → 核心插件 中确认 工作区 已启用。
1. 打开 设置 → 第三方插件 → 浏览，搜索 yuhanbo-workspaces。打开详情、核对名称和版本，按客户端的 安装 → 启用 操作。详情显示「禁用」时，说明当前已经启用。演示使用的是已安装状态。
1. 在 Windows 按 Ctrl+P 打开命令面板，搜索 打开工作区切换器，选中带 yuhanbo-workspaces 名称的命令。也可以从底部状态栏的工作区名打开列表。
![](https://xz.sanrenjz.com/image/%E5%AE%9E%E5%BD%95%E6%88%AA%E5%9B%BE-%E5%91%BD%E4%BB%A4%E5%85%A5%E5%8F%A3.png?imageSlim)

已启用原版 Workspaces Plus 时，先停用它，再启用本插件，避免两个插件同时接管工作区。最低支持 Obsidian 1.8.7。社区市场暂时不可用时，可以从同版本 Release 下载 main.js、manifest.json 和 styles.css，放入目标库的 .obsidian/plugins/yuhanbo-workspaces/，重新打开该库后启用。手动更新时保留已有的 data.json。

## 把会议和写作分别存成布局

* 先打开「会议议程」和「会议记录」，把它们放进两个并排的标签页分组。
* 从核心 工作区 的管理入口新建命名布局。已有布局要更新时，可以通过命令面板运行核心工作区的 保存布局。这个动作保存当前标签页和分组。
* 再安排「文章提纲」和「参考资料」，将它们存成另一套布局。通过 打开工作区切换器 搜索工作区名并按 Enter，或者点击对应条目。确认窗口重新显示该布局的笔记和分栏。
列表中的规模提示会统计布局内的标签页和 Markdown 笔记。30 篇及以上会提示「大型布局」。背景标签页由 Obsidian 在激活时按需加载。实际切换时间仍取决于布局规模、视图类型和同时运行的插件。

## 收藏、排序和复制

在 设置 → yuhanbo-workspaces → 工作区列表 打开某个工作区，开启 收藏此工作区。重新打开切换器，就能看到星标条目排在前面。个人工作区管理 → 工作区排序 可以把其他工作区按最近使用或名称排列。

要在原布局的基础上试另一种摆法，点 复制已保存布局。列表会增加一个副本，屏幕仍留在当前布局。临时打开且尚未保存的标签页不会进入副本。

![](https://xz.sanrenjz.com/image/%E5%AE%9E%E5%BD%95%E6%88%AA%E5%9B%BE-%E6%94%B6%E8%97%8F%E4%B8%8E%E5%89%AF%E6%9C%AC.png?imageSlim)

## 先备份，再改布局

在 个人工作区管理 → 工作区配置备份 点 创建备份，也可以运行 备份工作区配置 命令。默认保留最新 5 份。点 恢复备份 后先选择快照，确认页会说明覆盖范围。恢复会先尝试保存一份恢复前备份，然后更新同名工作区、补回缺失的工作区并保留其他条目。恢复后从切换器加载需要的布局。

备份保存在插件自己的本地数据文件中，内容是已保存的工作区配置。笔记正文仍由笔记库管理。教程现场创建了一份备份，并核对了恢复列表和确认提示。

## 按自己的习惯配置

| 选项 | 推荐先了解的行为 |
| --- | --- |
| 显示布局规模 | 默认开启，可在切换前查看标签页和笔记数量。 |
| 布局改变时自动保存当前工作区 | 默认关闭。想固定每套布局，就保留关闭并在确认改动后手动保存。 |
| 记住并恢复打开的文件 | 默认开启。保存布局时记录各标签页文件，切回时恢复。 |
| 切换时保留左右侧栏布局 / 侧边工具栏图标 | 默认关闭。希望不同工作区共用目前的侧栏或工具栏时，再按需开启。 |
| 启动时恢复上次工作区的已保存布局 | 默认关闭。开启后会应用已保存布局，上次未保存的布局变化可能被舍弃。 |
| 标签页文件覆盖 | 在单个工作区内设置。适合固定打开一份资料，文件覆盖优先于普通文件跟踪。 |
| 工作区模式 | 默认关闭，仅桌面端提供。它可以保存、切换部分 Obsidian 核心设置。 |Windows 默认可通过命令面板进入切换器。切换器内的 Enter 加载，Ctrl+Enter 重命名，Shift+Enter 保存，Ctrl+, 进入设置。是否显示数字提示取决于「切换列表的快捷键标记」配置。移动端用命令面板或启用侧边工具栏入口，本次仅实录 Windows。

## 操作流程回顾

先排好标签页并保存，再从切换器打开所需布局。常用布局设为收藏，需要试新排列时复制一份。大改之前创建本地配置备份。

![](https://xz.sanrenjz.com/image/%E6%B5%81%E7%A8%8B%E5%9B%BE-%E6%93%8D%E4%BD%9C%E6%B5%81%E7%A8%8B%E5%9B%9E%E9%A1%BE.png?imageSlim)

