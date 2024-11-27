### 用途说明

sync_folders 函数用于将源文件夹中的所有文件和子文件夹同步到目标文件夹，确保目标文件夹与源文件夹保持一致。如果目标文件夹不存在，则会自动创建。

### 参数

* source (str): 源文件夹的路径。
* destination (str): 目标文件夹的路径。
### 工作流程

```mermaid
graph TD
    A(开始) --> B{检查目标文件夹是否存在}
    B -- 不存在 --> C(创建目标文件夹)
    B -- 存在 --> D{遍历源文件夹}
    C --> D
    D --> E{计算相对路径}
    E --> F{创建目标子文件夹}
    F --> G{复制文件}
    G --> H{下一个文件/文件夹}
    H --> D
    H --> I(结束)
```

### 用法

通过传递源文件夹路径和目标文件夹路径来调用 sync_folders 函数。 该函数将同步源文件夹中的所有文件和子文件夹到目标文件夹。

### 示例

```python
import os
import shutil
import yuhanbolh as lh

def sync_folders(source, destination):
    # ... (函数代码)

# 示例用法
source_folder = "/path/to/source/folder"
destination_folder = "/path/to/destination/folder"
lh.sync_folders(source_folder, destination_folder)
```

在这个例子中，/path/to/source/folder 文件夹中的所有文件和子文件夹都会被同步到 /path/to/destination/folder 文件夹中.

