---
创建时间: 2023-12-10 10:05
修改时间: 2023-12-10 10:39
tags:
  - python
  - 完整代码
标题: Python自动化图像创作：调用阿里万象绘图api，生成图片
share: "true"
profileName: Default
postId: "4028"
categories:
  - 55
---


下面的代码是一个使用 Python 编写的脚本，用于调用阿里云的 Stable Diffusion 模型（通过 Dashscope 库）来生成图像。这个脚本显示了如何使用 Dashscope 的 API，根据用户提供的提示语句生成图像，并将它们保存到指定的路径。

```python
from http import HTTPStatus
from urllib.parse import urlparse, unquote
from pathlib import Path
from pathlib import PurePosixPath
import requests
import dashscope

# 阿里SD，500张，用完需再申请https://help.aliyun.com/zh/dashscope/developer-reference/getting-started-with-stable-diffusion-models?spm=5176.28197632.0.0.97d87e06OPIVDX&disableWebsiteRedirect=true

dashscope.api_key = ''

# model = "dashscope.ImageSynthesis.Models.wanx_v1"

def generate_and_save_images(prompt, n, size, save_path):
    rsp = dashscope.ImageSynthesis.call(model=dashscope.ImageSynthesis.Models.wanx_v1,
                                        prompt=prompt,
                                        n=n,
                                        size=size)
    if rsp.status_code == HTTPStatus.OK:
        print(rsp.output)
        print(rsp.usage)
        for result in rsp.output.results:
            file_name = PurePosixPath(unquote(urlparse(result.url).path)).parts[-1]
            save_file_path = Path(save_path) / file_name
            with open(save_file_path, 'wb+') as f:
                f.write(requests.get(result.url).content)
    else:
        print('Failed, status_code: %s, code: %s, message: %s' %
              (rsp.status_code, rsp.code, rsp.message))

if __name__ == '__main__':
    prompt = "a dog and a cat"
    n = 4
    size = '1024*1024'
    save_path = 'D:\\wenjian\\临时'
    generate_and_save_images(prompt, n, size, save_path)
```

# 代码解析

1. **导入所需库**: 使用http库处理HTTP状态。 urllib.parse用于解析和处理URL。 pathlib用于文件路径操作。 requests用于处理HTTP请求。 导入dashscope用于调用Stable Diffusion模型。
2. **设置API密钥和模型**: 需要将dashscope.api_key设置为有效的API密钥。
3. **定义generate_and_save_images函数**: 函数接受提示语句、生成数量、图像尺寸和保存路径作为参数。 使用Dashscope的ImageSynthesis.call方法调用Stable Diffusion模型。 根据返回的状态码处理结果，正确时保存生成的图像，错误时打印错误信息。
4. **图像保存逻辑**: 从返回的URL中提取文件名，并在指定路径保存图像。
5. **脚本主体**: 设置参数并调用generate_and_save_images函数。

![](https://mp.toutiao.com/mp/agw/article_material/open_image/get?code=MTNiOGNhZjQwNzlmM2I2Nzc0MDljYjBhNzM2NTRkMDgsMTcwMjE3NDc1OTI1MQ==)

# 代码的实际应用

这个脚本可以广泛应用于需要自动生成图像的场景，如：

- **内容创作**：为社交媒体、广告或网站自动生成图像内容。
- **艺术创作**：用于数字艺术和设计领域，根据创意提示生成图像。
- **数据可视化**：将抽象数据转换为直观的图像。

# 应用场景

- **商业营销**：用于快速生成营销材料中的视觉内容。
- **个人娱乐**：为个人项目或兴趣生成定制图像。
