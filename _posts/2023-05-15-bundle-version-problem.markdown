---
layout: post
title: "bundle version problem"
date: 2023-05-16 08:09:14 +0800
categories: solution
header-img: "img/post-bg.jpg"
header-mask: 0.3
---

## 使用bundle install时显示版本错误

### 问题描述

安装完Jekyll和bundler后，在博客项目中运行`bundle install`展示下面的报错

```(shell);
Bundler 2.4.13 is running, but your lockfile was generated with 2.3.22. Installing Bundler 2.3.22 and restarting using that version.
```

### 解决方法

重新安装提示版本的bundler

```(shell);
gem install bundler -v 2.3.22
```

重新运行`bundle install`正常
