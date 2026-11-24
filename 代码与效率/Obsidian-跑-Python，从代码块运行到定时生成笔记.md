程序小店：[程序小店 - obsidian插件-Yuhanbo Python Runner](https://shop.sanrenjz.com/obsidian/obsidian%E6%8F%92%E4%BB%B6-Yuhanbo-Python-Runner)

* [安装与使用文档（2.0.3）](https://github.com/yuhanbo758/obsidian-yuhanbo-python/blob/2.0.3/README.md)
* [Obsidian 社区插件页](https://community.obsidian.md/plugins/yuhanbo-python-runner)
* [实操视频（百家号）](https://mbd.baidu.com/newspage/data/videolanding?nid=sv_12535197982559818886)
* [实操视频（B 站）](https://www.bilibili.com/video/BV1ik1czaEzo/)
* [安装文件下载（GitHub Release 2.0.3）](https://github.com/yuhanbo758/obsidian-yuhanbo-python/releases/tag/2.0.3)
每周都要统计工时，先算总数，再算平均值，最后把结果整理进周报。脚本和周报通常分开存放。用 Yuhanbo Python Runner，可以把 Python 代码直接写进 Obsidian 笔记，临时需要时点一下运行，固定要做的事则交给定时任务，运行结果会存成一篇新的 Markdown 笔记。

下面用一份模拟周报演示。五天工时分别为 6、7、5、8、4 小时，预期得到总工时 30 小时、日均 6.0 小时，还有一行检查提示。用这三个结果可以逐步核对代码块、整篇运行和定时任务。

![](https://xz.sanrenjz.com/image/%E8%A7%86%E9%A2%91%E5%B0%81%E9%9D%A2_16%E6%AF%949_Obsidian%20Python%20%E8%87%AA%E5%8A%A8%E5%8C%96.png?imageSlim)

## 1. 安装插件，设置本地 Python

准备桌面版 Obsidian 1.7.2 或更高版本，以及本机的 Python 3。打开 设置 → 第三方插件 → 浏览，搜索 Yuhanbo Python Runner。进入详情页，点击 安装，再点击 启用。图中是已经安装的状态，客户端显示的可用版本和已安装版本都是 2.0.3。新版的中文作者署名为「余汉波」。

![](https://xz.sanrenjz.com/image/%E5%AE%9E%E6%8B%8D_%E7%A4%BE%E5%8C%BA%E6%90%9C%E7%B4%A2%E4%B8%8E%E5%AE%89%E8%A3%85.png?imageSlim)

打开 设置 → Yuhanbo Python Runner，检查 Python 路径。如果电脑能识别 python 命令，保留默认值即可。设置了虚拟环境，或运行时看到 ENOENT，填入对应解释器可执行文件的完整路径，例如 C:\Python312\python.exe。脚本所需的第三方库也应装进这个解释器所用的环境。本文示例只用 Python 标准库。

## 2. 在阅读模式运行一段代码

新建 周报助手.md，把下面两个代码块依次放进同一篇笔记。代码围栏的语言标记写作 python。

第一段计算总工时，并向标准错误流写一条检查提示。

```python
import sys

hours = [6, 7, 5, 8, 4]
print(f"本周总工时：{sum(hours)} 小时")
print("检查提示：周五低于 5 小时", file=sys.stderr)
```

第二段用同一组数据计算平均值。

```python
average = sum(hours) / len(hours)
print(f"日均工时：{average:.1f} 小时")
```

切到 阅读模式。第一个代码块下方的 复制 用来复制代码。点 运行，在 Python 执行结果 弹窗里能看到「本周总工时：30 小时」和检查提示。直接点 复制结果 会复制整段输出。只想带走其中一行，先在弹窗中选中文字，再点 复制结果。检查提示由示例主动写入 stderr，可用来确认插件同时展示两种输出流。

## 3. 从命令面板运行整篇笔记

第二段依赖第一段里的 hours。保持周报笔记打开，按 Ctrl+P（macOS 为 Cmd+P），在命令面板搜索并选择 Yuhanbo Python Runner: 运行当前文件中的Python代码。插件按笔记中的顺序组合代码块，结果里就会同时出现总工时和日均工时。

如果经常用整篇执行，可以到 设置 → 快捷键，搜索这条命令并绑定一个顺手的按键。

## 4. 添加定时任务，让结果自动成为笔记

先在库里建一个 输出 文件夹。打开 设置 → Yuhanbo Python Runner → 添加定时任务，按以下内容填写。

| 设置项 | 周报示例 |
| --- | --- |
| MD文件路径 | 选择已保存的 周报助手.md |
| 输出路径 | 选择库里的 输出 文件夹 |
| 执行频率 | 初次验证选 单次执行，再选日期 |
| 执行时间 | 用 24 小时制，设在几分钟后 |
| 输出文件名 | 填 周报运行结果-新版.md，留空时使用默认的 {timestamp}.md |保存后保持 Obsidian 打开。任务触发后，在侧栏展开 输出，打开 周报运行结果-新版.md。这次在测试库里实际生成的笔记含有总工时、平均工时和检查提示。验证完成后，固定每天运行可以选 每日执行，固定星期几运行可以选 每周执行，并指定星期几。

![](https://xz.sanrenjz.com/image/%E5%AE%9E%E6%8B%8D_%E5%AE%9A%E6%97%B6%E7%94%9F%E6%88%90%E7%9A%84%E5%91%A8%E6%8A%A5.png?imageSlim)

![](https://xz.sanrenjz.com/image/%E6%B5%81%E7%A8%8B%E5%9B%BE_%E8%BF%90%E8%A1%8C%E4%B8%8E%E5%AE%9A%E6%97%B6%E4%BF%9D%E5%AD%98.png?imageSlim)

以后要整理 CSV 摘要、汇总每周学习记录，或从本地数据生成 Markdown，沿用这套流程即可。先手动跑一遍，确认输出符合预期，再设置定时任务。Python 按 Obsidian 进程的系统权限运行，请只运行可信来源的代码。

