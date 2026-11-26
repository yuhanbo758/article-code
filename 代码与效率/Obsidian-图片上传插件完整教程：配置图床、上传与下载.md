程序小店：[程序小店 - obsidian插件-yuhanbo-image-upload，图片上传](https://shop.sanrenjz.com/obsidian/obsidian%E6%8F%92%E4%BB%B6-yuhanbo-image-upload%EF%BC%8C%E5%9B%BE%E7%89%87%E4%B8%8A%E4%BC%A0)

bili 视频：[Obsidian 图片上传插件完整教程：配置图床、上传与下载_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1vFymz9Ekx/?vd_source=247ac77d4ae7339ea06d0fec09aa8f70)

* [安装与使用文档](https://github.com/yuhanbo758/obsidian-yuhanbo-image_upload/blob/main/README-zh.md)
* [下载插件文件（GitHub Release）](https://github.com/yuhanbo758/obsidian-yuhanbo-image_upload/releases/latest)
* [Obsidian 社区插件页](https://community.obsidian.md/plugins/yuhanbo-image-upload)
一篇笔记里既有本地截图，又有早已发布的网络图时，怎样批量上传并保留原有链接？桌面插件 yuhanbo-image-upload 可以一次上传整篇笔记里的本地图，也能通过右键只上传一张。网络图需要离线查看时，还能把它们保存回笔记库。

![](https://xz.sanrenjz.com/image/%E8%A7%86%E9%A2%91%E5%B0%81%E9%9D%A2_16%E6%AF%949_Obsidian%20%E5%9B%BE%E7%89%87%E4%B8%8A%E4%BC%A0.png?imageSlim)

## 整篇上传与右键单传

打开一篇含本地图和网络图的笔记，按 Ctrl+P，在命令面板运行 yuhanbo-image-upload: Upload all images。插件会识别 Wiki 图片嵌入和标准 Markdown 图片。上传成功的本地引用会换成图床链接，已有的网络图继续使用原地址，上传失败的本地图仍引用原文件。多处引用同一个附件时，附件只上传一次。

视频里，「图片上传演示库」中的两张本地图上传成功，原网络图保持原地址。切到源码可核对两条新链接，切回预览仍能看到三张图。

![](https://xz.sanrenjz.com/image/%E5%AE%9E%E5%BD%95%E6%88%AA%E5%9B%BE-%E6%89%B9%E9%87%8F%E4%B8%8A%E4%BC%A0%E7%BB%93%E6%9E%9C.png?imageSlim)

只传一张时，在实时预览中右键点击目标图片，选择 上传图片。在笔记右上角切换到源码模式，可以直接看到哪一条引用已经更新。

![](https://xz.sanrenjz.com/image/%E5%AE%9E%E5%BD%95%E6%88%AA%E5%9B%BE-%E5%8F%B3%E9%94%AE%E4%B8%8A%E4%BC%A0.png?imageSlim)

## 粘贴、拖拽与单篇设置

* 粘贴截图。打开插件设置里的「剪切板自动上传」。将图像粘贴到编辑区，成功后会在光标处插入图床链接。Excel 等软件可能同时提供文本和图像，插件设置里有对应的开关。
* 拖入图片。使用 PicGo 或 PicList 桌面服务时，可以从资源管理器把本地图片拖入编辑区。Windows 下按住 Ctrl 拖入，可以让 Obsidian 按本地附件处理。
* 单篇笔记停用自动上传。在笔记属性中添加 image-auto-upload，类型选「复选框」，取消勾选。也可以在源码模式写入布尔值 image-auto-upload: false。其他笔记继续使用插件设置。
* 重新上传剪贴板中的网络图。打开「应用网络图片」后，插件可以处理粘贴进来的 Markdown 网络图片链接。用「网络图片域名黑名单」排除指定域名，多个域名用英文逗号分隔。
## 多篇笔记共用图片时一起换链

几篇笔记有时引用同一个本地附件。把「其他笔记替换成网络图片」打开，在其中一篇执行 Upload all images，引用同一附件的其他笔记也会使用同一个图床链接。开关默认关闭，右键单传始终只更新当前笔记。操作后可以打开另一篇笔记检查源码里的地址。

## 把网络图下载回笔记库

在目标笔记运行 yuhanbo-image-upload: Download all images。成功下载的文件会保存到笔记库，对应网络链接会换成库内附件路径。可以从源码中打开附件，再到文件列表确认它确实已保存在本地。

## 连接 PicGo、PicList 或 PicGo-Core

先在上传器中配置图床，再进入 Obsidian「设置 → yuhanbo-image-upload」。初次配置完成后，先选一张可以公开的测试图上传，确认返回的图片地址可访问。

| 使用方式 | Obsidian 配置 |
| --- | --- |
| 本机 PicGo 桌面版 | 启动上传服务，默认上传器选 PicGo(app)。本机默认上传接口通常为 http://127.0.0.1:36677/upload。 |
| 本机 PicList 桌面版 | 同样选择 PicGo(app)，填写 PicList 实际监听的上传接口。需要指定图床和配置时可按 PicList 文档使用 picbed 和 configName 参数。 |
| 自建远程 PicList 或 PicList-Core | 打开「远程服务器模式」，填入远程上传接口。插件会把所选图片发送给配置的服务。 |
| 本机 PicGo-Core | 选择 PicGo-Core，按需填入其命令路径。留空时从系统路径查找。 |![](https://xz.sanrenjz.com/image/%E5%AE%9E%E5%BD%95%E6%88%AA%E5%9B%BE-%E4%B8%8A%E4%BC%A0%E5%99%A8%E8%AE%BE%E7%BD%AE.png?imageSlim)

图片描述和图片大小后缀会影响新插入的图片引用。需要保留原图时，保持「上传文件后移除源文件」关闭。PicGo server 删除接口仅用于支持删除操作的 PicList 配置。

## 安装和启用

在桌面版 Obsidian 打开「设置 → 第三方插件 → 浏览」，搜索 yuhanbo-image-upload，进入作者为 余汉波 的插件详情。首次使用时点击「安装」并启用。需要手动安装时，从 GitHub Release 下载同一版本的 main.js 和 manifest.json，放在目标笔记库的 .obsidian/plugins/yuhanbo-image-upload/，再在「第三方插件」启用。

![](https://xz.sanrenjz.com/image/%E6%B5%81%E7%A8%8B%E5%9B%BE-%E6%93%8D%E4%BD%9C%E5%9B%9E%E9%A1%BE.png?imageSlim)

实操使用 Windows 桌面版 Obsidian 1.15.1、插件 4.2.2、「图片上传演示库」和本地 PicGo 兼容测试接口。上线使用时，按自己的上传器配置填写接口。

