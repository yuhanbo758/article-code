---
创建时间: 2024-02-01 22:02
修改时间: 2024-02-01 22:03
tags:
  - python
  - 文件处理
标题: youtube批量上传
share: "true"
---


在 Python 中实现 YouTube 批量上传，你可以使用 Google 的 YouTube Data API v3 和 Google OAuth 2.0 来认证和上传视频。以下是一个基础的实现流程，包括如何设置、认证和上传视频的示例代码。

### 第一步：设置

1. 在 [Google Cloud Console](https://console.developers.google.com/) 中创建一个新项目。
2. 启用 YouTube Data API v3。
3. 创建 OAuth 2.0 凭证（客户端 ID 和客户端密钥）。
4. 下载凭证，保存为 `client_secrets.json`。

### 第二步：安装所需库

安装 Google API 客户端库和 Google OAuth 库：

```bash
pip install --upgrade google-api-python-client google-auth google-auth-oauthlib google-auth-httplib2
```

### 第三步：认证和上传脚本

创建一个 Python 脚本（`upload_videos.py`），使用以下代码：

```python
import os
import google.oauth2.credentials
import google_auth_oauthlib.flow
from googleapiclient.discovery import build
from googleapiclient.errors import HttpError
from google_auth_oauthlib.flow import InstalledAppFlow
from googleapiclient.http import MediaFileUpload

# 需要打开VPN的TUN模式


# 设置OAuth 2.0的范围和视频文件路径
SCOPES = ['https://www.googleapis.com/auth/youtube.upload']
API_SERVICE_NAME = 'youtube'
API_VERSION = 'v3'


def get_authenticated_service():
    flow = InstalledAppFlow.from_client_secrets_file(
        r"D:\wenjian\临时\client_secrets.json", SCOPES)
    credentials = flow.run_local_server(port=0)
    return build(API_SERVICE_NAME, API_VERSION, credentials=credentials)


def initialize_upload(youtube, options):
    body = {
        'snippet': {
            'title': options['title'],
            'description': options['description'],
            'tags': options['tags'],
            'categoryId': options['category']
        },
        'status': {
            'privacyStatus': options['privacyStatus'],
            # 确保此处直接设置madeForKids属性
        },
        # 直接在body的顶层设置'madeForKids'
        'madeForKids': False,
    }

    insert_request = youtube.videos().insert(
        part=','.join(body.keys()) + ',status',  # 确保status也被包含在part参数中
        body=body,
        media_body=MediaFileUpload(options['file'], chunksize=-1, resumable=True)
    )

    return insert_request.execute()


def upload_videos(video_files):
    youtube = get_authenticated_service()
    for video_file in video_files:
        try:
            print(f"Uploading file: {video_file['file']}")
            initialize_upload(youtube, video_file)
        except HttpError as e:
            print(f"An HTTP error {e.resp.status} occurred:\n{e.content}")
        else:
            print("Upload successful.")

if __name__ == '__main__':
    video_files = [
        {
            'file': r"D:\自媒体\剪辑\发表视频\阅读驴友\静夜思：李白笔下的月光、乡愁与无尽思绪.mp4",
            'title': '静夜思：李白笔下的月光、乡愁与无尽思绪',
            'description': '静夜思：李白笔下的月光、乡愁与无尽思绪',
            'category': '27',  # 教育类别
            'tags': ['李白', '静夜思', '古诗鉴赏'],
            'privacyStatus': 'public',
            'madeForKids': False,  # 直接在这里设置，而不是嵌套在'status'字典内
        },
        # 添加更多视频
    ]

    upload_videos(video_files)



```

在这个脚本中，你需要替换 `video_files` 列表中的视频信息，包括文件路径、标题、描述等。另外，确保已经安装了 `google-auth-oauthlib` 和 `google-api-python-client` 库来处理认证和 API 调用。

请注意，由于 YouTube 上传视频需要经过认证，这个脚本会在首次运行时打开一个新的浏览器窗口或者给出一个 URL 让你完成 OAuth 2.0 认证流程。认证成功后，脚本会保存认证信息以便下次使用。

### 注意事项

- 此代码示例仅为基础实现，可能需要根据你的具体需求进行调整。
- 确保遵守 YouTube API 使用条款和限制。
- 考虑到 API 调用次数的限制，计划好批量上传操作，避免达到日限额。
