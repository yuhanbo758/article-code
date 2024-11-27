### 用途说明

本函数用于将本地文件上传至Lsky Pro，并根据设定的策略ID返回对应的Markdown链接。当策略ID为2时，返回minlo图床的链接。

### 参数

* file_path (str):  要上传的本地文件路径。
### 用法

调用 upload_to_lsky_pro(file_path) 上传文件并获取Markdown链接。

### 示例

```python
file_path = "/path/to/your/file.jpg"
markdown_link = upload_to_lsky_pro(file_path)
print(f"文件上传成功，Markdown 链接为：{markdown_link}")
```

### 流程图

```mermaid
graph TD
    A[开始] --> B{读取文件}
    B --> C{设置请求头和请求体}
    C --> D{发送上传请求}
    D --> E{判断响应状态码}
    E -- 200 --> F{解析响应数据}
    E -- 其他 --> G{抛出异常}
    F --> H{判断上传是否成功}
    H -- 成功 --> I{返回Markdown链接}
    H -- 失败 --> G
    G --> J[结束]
    I --> J
```

