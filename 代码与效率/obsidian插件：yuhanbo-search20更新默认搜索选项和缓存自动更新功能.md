yuhanbo-search1.0 的文章和视频详情请前往： [obsidian插件：yuhanbo--search，自定义加权的内容搜索插件 | 余汉波 文档](https://wd.sanrenjz.com/%E4%BB%A3%E7%A0%81%E4%B8%8E%E6%95%88%E7%8E%87/obsidian%E6%8F%92%E4%BB%B6%EF%BC%9Ayuhanbo--search%EF%BC%8C%E8%87%AA%E5%AE%9A%E4%B9%89%E5%8A%A0%E6%9D%83%E7%9A%84%E5%86%85%E5%AE%B9%E6%90%9C%E7%B4%A2%E6%8F%92%E4%BB%B6)

bili 视频：[obsidian插件：yuhanbo-search2.0，更新默认搜索选项和缓存自动更新功能_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1QLMiz4ELp/?vd_source=247ac77d4ae7339ea06d0fec09aa8f70#reply114692605347007)

程序小店： [obsidian插件：加权搜索yuhanbo-search2.0 | 三人聚智-余汉波程序小店](https://jy.sanrenjz.com/buy/32)

github：[yuhanbo758/obsidian-yuhanbo-search: obsidian的搜索搜索，主要功能是解决搜索加权的问题，可以自行设置标题、属性、引用等的加权搜索](https://github.com/yuhanbo758/obsidian-yuhanbo-search)

### 1. 修改默认搜索选项

在 main.js 的 SearchModal 构造函数中，将默认搜索选项调整为：

* ✅ 文件名 (fileName: true)
* ✅ 目录 (directory: true)
* ✅ 标签 (tags: true)
* ✅ 标题 (headings: true)
* ❌ 内容 (content: false) - 改为默认关闭
* ❌ 引用 (quotes: false) - 改为默认关闭
![](https://xz.sanrenjz.com/image/Pasted%20image%2020250616080254.png?imageSlim)

### 2. 修改插件加载逻辑和增加设置自动更新缓存

在 onload 方法中实现了条件逻辑（可以设置中进行打开或关闭）：

* 开启自动更新时 ：
* 关闭自动更新时 ：
[[obsidian插件：yuhanbo--search，自定义加权的内容搜索插件]]

