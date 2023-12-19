---
创建时间: 2023-12-09 09:37
修改时间: 2023-12-09 12:13
tags:
  - python
  - 完整代码
标题: 如何用Python高效地分割PDF文件：一个简洁的PyPDF2脚本解析
其他: 
profileName: Default
postId: "4013"
categories:
  - 55
share: "true"
---


这段代码的核心功能是将一个 PDF 文件分割成多个较小的 PDF 文件，每个文件包含指定数量的页面。这个功能对于处理大型 PDF 文件非常有用，尤其是当需要单独处理或分发文件的特定部分时。

```python

import os
from PyPDF2 import PdfReader, PdfWriter

def split_pdf(file_path, pages_per_file):
    # 打开原始PDF文件
    with open(file_path, 'rb') as infile:
        reader = PdfReader(infile)
        total_pages = len(reader.pages)

        # 创建与原文件同名的新文件夹
        file_dir, file_name = os.path.split(file_path)
        file_base, file_ext = os.path.splitext(file_name)
        new_folder_path = os.path.join(file_dir, file_base)
        if not os.path.exists(new_folder_path):
            os.makedirs(new_folder_path)

        # 分割PDF
        for start_page in range(0, total_pages, pages_per_file):
            writer = PdfWriter()
            end_page = min(start_page + pages_per_file, total_pages)

            for page in range(start_page, end_page):
                writer.add_page(reader.pages[page])

            output_filename = os.path.join(new_folder_path, f"{file_base}_{start_page // pages_per_file + 1}{file_ext}")

            with open(output_filename, 'wb') as outfile:
                writer.write(outfile)

# 使用示例
split_pdf(r"D:\wenjian\临时\斗破苍穹.pdf", 500)  # 这里5是每个分割文件的页面数
```

### 代码解析

1. **函数定义**:
    - `split_pdf(file_path, pages_per_file)`: 这个函数用于分割PDF文件。它接受两个参数：PDF文件的路径（`file_path`）和每个分割文件中应包含的页面数（`pages_per_file`）。
2. **打开原始PDF文件**:
    - 使用`PdfReader`从PyPDF2库中读取PDF文件。
3. **创建新文件夹**:
    - 从原文件路径提取文件名和目录。
    - 在原文件所在的目录中创建一个新的文件夹，以存放分割后的PDF文件。
4. **分割PDF文件**:
    - 使用循环，每次迭代处理`pages_per_file`指定的页面数。
    - 对于每个分割文件，使用`PdfWriter`创建一个新的PDF文件，并添加相应的页面。
    - 每个分割文件以原文件名开始，并附加一个基于其在原文件中位置的编号。
5. **写入分割文件**:
    - 将分割后的PDF内容写入新文件。

### 代码的实际应用

这个脚本在各种情景下都非常有用，特别是在需要处理大型PDF文件的场景中。例如：

- **教育和培训**：教师可以将大型教材或课程资料分割成小节，方便学生阅读和下载。
- **工作场所**：在需要分享或协作处理大型报告或文档的时候，可以将其分割成更易于管理的小部分。
- **个人使用**：对于阅读大型电子书或手册时，分割成小部分可以使阅读和引用更加方便。

### 应用场景

- **分割长文档**：将长篇幅的报告或书籍分割成章节或部分，以便单独阅读或分享。
- **创建小册子**：将大型文件分割成小册子格式，方便打印和分发。
