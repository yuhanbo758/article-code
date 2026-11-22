* [安装与使用文档](https://github.com/yuhanbo758/obsidian-yuhanbo-autocomplete#使用)
* [实操视频（百家号）](https://mbd.baidu.com/newspage/data/videolanding?nid=sv_2113174925477484216)
* [实操视频（B 站）](https://www.bilibili.com/video/BV1TJyLzQE3E/)
* [安装文件下载（GitHub Release）](https://github.com/yuhanbo758/obsidian-yuhanbo-autocomplete/releases/latest)
https://f7.baidu.com/it/u=2037782966,1480562757&fm=222&app=106&f=PNG

写项目笔记时经常重复输入「提示词」「项目回顾」之类的表达。yuhanbo-autocomplete 会在编辑器光标附近给出候选，选择后即可补全。它优先支持中文，同时可以补全英文术语、笔记链接和自己的固定短语。

## 输入前缀，选中候选

打开一篇笔记，切换到编辑视图，把光标放在正文中。

1. 输入并提交「提示」，观察光标旁的候选。若出现「提示词」，可直接点该候选插入。
1. 换一行输入 autoc，用同样的方法选择 autocomplete。候选会受当前笔记、历史和设置影响。
1. 中文输入法还在组词时，插件默认暂停弹出候选。先选字或提交整词，再观察 Obsidian 的建议列表。这两个候选窗口分别由输入法和插件控制。
若没看到建议，先确认当前是编辑视图、插件已启用，再查看插件设置中的自动触发和最少触发字符数。把光标留在前缀后，按 Ctrl+P 打开 Windows 命令面板，执行「yuhanbo-autocomplete：显示补全建议」。候选出现后可按回车接受当前项，或点击其他候选。库内同时启用多个自动补全插件时，建议只启用需要使用的那个。

## 输入文件名前缀，直接插入双链

开启插件设置中的「启用内部链接补全」后，在正文输入已有 Markdown 笔记的文件名前缀。演示输入 2026，从候选里选中「2026 项目复盘（演示）」，插件写入 [[2026 项目复盘（演示）]]。候选名称下方显示对应的 Markdown 文件。把光标留在链接处，Windows 上按 Ctrl+Enter 可以打开目标笔记，然后切回原标签页继续编辑。

![](https://xz.sanrenjz.com/image/%E5%AE%9E%E5%BD%95%E6%88%AA%E5%9B%BE-%E5%8F%8C%E9%93%BE%E5%80%99%E9%80%89.png?imageSlim)

## 把常写的一整句存成词库

在当前笔记库的 自动补全视频示例 子文件夹创建 演示词库.txt，使用 UTF-8，每行一条。示例包含两条常用短语。

```vb.net
三人聚智写作练习
每周项目回顾
```

打开 设置 → yuhanbo-autocomplete，打开「启用自定义词库」开关，把 自动补全视频示例/演示词库.txt 填入「自定义词库路径」。路径从笔记库根目录算起，多个文件每行填一个路径。回到编辑器，输入「每周」，在候选里选择「每周项目回顾」。修改词库后先保存 TXT，再回到笔记，在命令面板执行「yuhanbo-autocomplete：重新加载词库」，最后用同一前缀检查新条目。

## 按需要开启更多候选来源

插件可以使用当前笔记中的词语、笔记链接、自定义词库等来源。若希望其他笔记里的词也参与补全，可在插件设置里开启全库词语补全，并按需排除目录。用单独的词库维护固定短语，适合希望候选更集中、更可控的场景。

默认补全与中文分词在本地运行。只有主动配置并启用远程词库 URL 时，插件才会向该地址请求下载词库。

## 从社区市场安装

在 Obsidian 设置 → 第三方插件 → 浏览中搜索 yuhanbo-autocomplete。核对名称和作者 yuhanbo，打开详情并点「安装」，安装完成后点「启用」。如果插件已经安装，详情页会显示已安装。现有用户可从这里检查更新。

![](https://xz.sanrenjz.com/image/%E5%AE%9E%E5%BD%95%E6%88%AA%E5%9B%BE-%E7%A4%BE%E5%8C%BA%E5%B8%82%E5%9C%BA.png?imageSlim)

画面来自 Windows 上 Obsidian 1.15.1 的测试库实录。详情显示当前已安装并启用 1.0.9。

![](https://xz.sanrenjz.com/image/%E6%B5%81%E7%A8%8B%E5%9B%BE-%E6%93%8D%E4%BD%9C%E5%9B%9E%E9%A1%BE.png?imageSlim)

插件要求 Obsidian 1.11.4 或更高版本。市场安装之外，也可从 GitHub 下载同一版本的 main.js、manifest.json、styles.css，一并放入笔记库的 .obsidian/plugins/autocomplete/，再启用插件。项目基于 tadashi-aikawa 的 Various Complements，沿用 MIT 许可证，并经原作者公开同意提交社区市场。

[Obsidian 社区页面](https://community.obsidian.md/plugins/autocomplete) · [GitHub 正式版本](https://github.com/yuhanbo758/obsidian-yuhanbo-autocomplete/releases/tag/1.0.9)

