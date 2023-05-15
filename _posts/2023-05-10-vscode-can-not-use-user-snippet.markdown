---
layout: post
title: 'VScode can not use user snippet'
date: 2022-09-22 23:02:57 +0800
categories: solution
header-img: "img/post-bg.jpg"
header-mask: 0.3
---

## VScode配置了用户代码片段但不生效

问题描述：在VScode中配置了用户代码片段，但输入对应的prefix后没有提示。

### 1. 配置用户代码片段

点击`文件`，点击`首选项`，点击`用户代码片段`，选择`markdown.json`

配置以下代码片段:

```(json);
"Insert code snippet": {
"prefix": "codes",
"body": [
  "```($1);",
  "$2",
  "```"
],
"description": "Insert code snippet"
}
```

### 2. 修改配置开启markdown类型文件中的键入提示

通过快捷键`ctrl+shift+P`显示所有命令，选择`打开用户设置(JSON)`，增加以下配置：

```(json);
"[markdown]": {
    "editor.quickSuggestions": {
      "comments": "on",
      "strings": "on",
      "other": "on"
    },
  },
```
