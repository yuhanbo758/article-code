---
创建时间: <% tp.file.creation_date() %>
修改时间: <% tp.file.last_modified_date() %>
tags:
  - python
标题: <% tp.file.title %>
share: "true"
---

<% await tp. file. move ("/学习阅读/学习/效率工具/Python/" + ((tp. file. title. includes ("未命名") || tp. file. title. toLowerCase (). includes ("untitled")) ? (await tp. system. prompt ("请输入要创建的文件名")) : tp. file. title)) %>