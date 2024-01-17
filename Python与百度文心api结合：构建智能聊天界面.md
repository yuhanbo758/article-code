---
创建时间: 2023-12-10 09:29
修改时间: 2023-12-10 10:04
tags:
  - python
  - 完整代码
标题: Python与百度文心api结合：构建智能聊天界面
share: "true"
profileName: Default
postId: "4032"
categories:
  - 55
---



下面代码是一个基于 Python 和 Tkinter 库，结合百度智能云 API 的聊天机器人界面。此程序通过图形用户界面与用户交互，将用户输入的消息发送到百度智能云进行处理，并展示返回的结果。这个示例展现了如何将先进的自然语言处理技术与用户友好的界面相结合，创造出交互式的聊天体验。

```
import requests
import json
import tkinter as tk
import tkinter.font as tkFont
from tkinter import scrolledtext, Label, Entry, StringVar

# 请确保将 API Key 和 Secret Key 替换为您自己的
API_KEY = ''
SECRET_KEY = ''



def get_access_token(api_key, secret_key):
    url = "https://aip.baidubce.com/oauth/2.0/token"
    params = {
        "grant_type": "client_credentials",
        "client_id": api_key,
        "client_secret": secret_key
    }
    response = requests.post(url, params=params)
    return response.json().get("access_token")

dialogue_history = []  # 用于存储对话历史的全局变量

def send_request():
    global dialogue_history
    access_token = get_access_token(API_KEY, SECRET_KEY)
    if not access_token:
        update_display("无法获取访问令牌。", {})
        return

    user_input = messages_input.get("1.0", tk.END).strip()
    if user_input:
        dialogue_history.append({"role": "user", "content": user_input})

    # 确保历史对话信息的总长度不超过限制
    # 如有需要，从早期对话开始删除，直到满足条件
    while len(json.dumps(dialogue_history)) > 4800:
        dialogue_history.pop(0)

    url = f"https://aip.baidubce.com/rpc/2.0/ai_custom/v1/wenxinworkshop/chat/completions_pro?access_token={access_token}"
    headers = {'Content-Type': 'application/json'}
    payload = {
        "messages": dialogue_history,
        'temperature': float(temperature_var.get()),
        'top_p': float(top_p_var.get()),
        'penalty_score': float(penalty_score_var.get()),
        "stream": stream_var.get() == 'False',
        'system': system_var.get(),
    }

    try:
        response = requests.post(url, headers=headers, data=json.dumps(payload))
        response.raise_for_status()

        if response.text:
            response_data = response.json()
            bot_response = response_data.get('result', "没有返回结果")
            if bot_response:
                dialogue_history.append({"role": "assistant", "content": bot_response})
                update_display(bot_response, response_data.get('usage', {}))
            else:
                update_display("没有返回结果。", {})
        else:
            update_display("API没有返回数据。", {})

    except requests.exceptions.HTTPError as http_err:
        update_display(f"HTTP错误：{http_err}", {})
    except requests.exceptions.RequestException as err:
        update_display(f"请求错误：{err}", {})
    except json.JSONDecodeError:
        update_display("无法解析JSON响应。", {})

    # 清空输入框内容
    messages_input.delete("1.0", tk.END)




def update_display(result, usage):
    # 更新结果显示框
    result_output.config(state=tk.NORMAL)
    result_output.delete("1.0", tk.END)
    result_output.insert(tk.END, result if result else "没有返回结果")
    result_output.config(state=tk.DISABLED)
    
    # 更新使用情况显示框
    usage_output.config(state=tk.NORMAL)
    usage_output.delete("1.0", tk.END)  # 清除初始提示文本或之前的内容
    usage_output.insert(tk.END, json.dumps(usage, indent=4) if usage else "没有使用数据")
    usage_output.config(state=tk.DISABLED)


def on_send_button_click(event=None):
    send_request()
    # 清空输入框内容
    messages_input.delete("1.0", tk.END)


def copy_to_clipboard():
    root.clipboard_clear()  # 清除剪贴板内容
    root.clipboard_append(result_output.get("1.0", tk.END))  # 将结果复制到剪贴板


def get_system_input():
    return system_input.get("1.0", tk.END).strip()  # 获取所有文本并去除首尾空白字符



root = tk.Tk()
root.title("文心一言4.0")

# 创建输出框，并设置默认字体大小
result_output = scrolledtext.ScrolledText(root, height=10, width=50, state='disabled', font=("Helvetica", 14))
result_output.grid(row=0, column=0, padx=10, pady=10, sticky="nsew")


# 占位符文本
placeholder = "请输入问题，可通过shift+回车换行"

# 创建输入框，并设置默认字体大小
messages_input = scrolledtext.ScrolledText(root, height=5, width=50, font=("Helvetica", 14))
messages_input.grid(row=3, column=0, padx=10, pady=10, sticky="nsew")
messages_input.insert(tk.END, placeholder)

# 输入框的占位符逻辑
def on_focus_in(event):
    if messages_input.get("1.0", "end-1c") == placeholder:
        messages_input.delete("1.0", "end")
        messages_input.config(fg='black')

def on_focus_out(event):
    if not messages_input.get("1.0", "end-1c"):
        messages_input.insert("1.0", placeholder)
        messages_input.config(fg='grey')

# 绑定焦点事件
messages_input.bind("<FocusIn>", on_focus_in)
messages_input.bind("<FocusOut>", on_focus_out)

# 初始化输入框为灰色字体
messages_input.config(fg='grey')


# 清除历史记录的函数
def clear_history():
    global dialogue_history
    dialogue_history.clear()  # 清空对话历史
    result_output.config(state=tk.NORMAL)
    result_output.delete("1.0", tk.END)  # 清空结果输出框
    result_output.config(state=tk.DISABLED)
    usage_output.config(state=tk.NORMAL)
    usage_output.delete("1.0", tk.END)  # 清空使用情况输出框
    usage_output.config(state=tk.DISABLED)



# 创建参数输入字段
temperature_var = StringVar(value='0.8')
top_p_var = StringVar(value='0.8')
penalty_score_var = StringVar(value='1.0')
stream_var = StringVar(value='True')
system_var = StringVar()

params_frame = tk.Frame(root)
params_frame.grid(row=0, column=1, rowspan=6, sticky='ns')

Label(params_frame, text="随机").grid(row=0, column=0, sticky='e')
Entry(params_frame, textvariable=temperature_var).grid(row=0, column=1, sticky='ew')

Label(params_frame, text="多样").grid(row=1, column=0, sticky='e')
Entry(params_frame, textvariable=top_p_var).grid(row=1, column=1, sticky='ew')

Label(params_frame, text="惩罚").grid(row=2, column=0, sticky='e')
Entry(params_frame, textvariable=penalty_score_var).grid(row=2, column=1, sticky='ew')

Label(params_frame, text="流式").grid(row=3, column=0, sticky='e')
Entry(params_frame, textvariable=stream_var).grid(row=3, column=1, sticky='ew')

Label(params_frame, text="人设").grid(row=4, column=0, sticky='e')

# 将原先的Entry控件更改为Text控件
system_input = tk.Text(params_frame, height=6, width=2, wrap='word')  # 设置高度足够容纳多行文字，并设置自动换行
system_input.grid(row=4, column=1, sticky='ew')

# 在界面中创建复制按钮
copy_button = tk.Button(root, text="复制", command=copy_to_clipboard)
copy_button.grid(row=2, column=0, padx=10, pady=10, sticky="ew")



# 创建使用输出字段
usage_output = scrolledtext.ScrolledText(params_frame, height=8, width=5, state='normal')  # 临时设置state为normal以插入文本
usage_output.grid(row=5, column=0, columnspan=2, padx=10, pady=10, sticky="ew")
# 配置tag来设置灰色字体
usage_output.tag_configure('gray', foreground='gray')
# 插入初始提示文本并应用灰色字体
usage_output.insert(tk.END, "计算token...", 'gray')
usage_output.config(state='disabled')  # 再次设置为disabled以防止编辑


# 创建发送按钮
send_button = tk.Button(root, text="发送", command=on_send_button_click)
send_button.grid(row=6, column=0, padx=10, pady=10, sticky="ew")

# 创建清除记录按钮
clear_button = tk.Button(root, text="清除记录", command=clear_history)
clear_button.grid(row=6, column=1, padx=10, pady=10, sticky="ew")


# 设置窗口的宽度、高度和位置
window_width = 800
window_height = 600

# 获取屏幕尺寸以计算布局参数，使窗口居中
screen_width = root.winfo_screenwidth()
screen_height = root.winfo_screenheight()

# 计算x和y坐标以使窗口居中
x = (screen_width / 2) - (window_width / 2)
y = (screen_height / 2) - (window_height / 2)
root.geometry('%dx%d+%d+%d' % (window_width, window_height, x, y))

# 绑定Enter键到on_send_button_click函数
root.bind('<Return>', on_send_button_click)

# 设置列和行权重，使界面在调整大小时能很好地调整
root.grid_columnconfigure(0, weight=3)  # Message column
root.grid_columnconfigure(1, weight=1)  # Parameter and usage column
root.grid_rowconfigure(0, weight=1)     # For messages and result display

root.mainloop()
```

# 代码解析

1. **导入必要的库**: 使用requests进行HTTP请求，json处理数据，tkinter和tkinter.font构建图形界面。
2. **API密钥和令牌获取**: 使用get_access_token函数从百度智能云获取访问令牌。
3. **聊天记录管理**: dialogue_history全局变量用于存储对话历史。 send_request函数处理用户输入，维护对话历史并调用API。
4. **构建GUI应用程序**: SparkChatbotGUI类负责创建和管理GUI应用程序的各个组件，包括文本显示区域、输入框、参数设置区域和按钮。
5. **API调用与数据处理**: 用户输入被发送到百度智能云API，返回的响应在GUI上显示。 使用异常处理来管理API调用中可能出现的错误。
6. **用户交互和可视化**: 通过输入框接收用户输入，结果输出区显示响应。 提供清除历史、复制到剪贴板等附加功能。

# 代码的实际应用

此聊天机器人应用程序在多种场合都非常有用，例如：

- **客户支持**：作为前端接口，回答常见问题或提供信息。
- **教育工具**：辅助教学，提供互动式学习体验。
- **个人助理**：执行简单任务，如设置提醒、查询信息等。

# 应用场景

- **商业应用**：作为企业网站或应用程序的一部分，提高客户互动效率。
- **社交娱乐**：用于社交媒体平台，提供有趣的对话体验。
