---
layout: post
title: 'Try to build my awesome jekyll theme'
date: 2022-09-22 23:02:57 +0800
categories: jekyll update
header-img: "img/post-bg.jpg"
header-mask: 0.3
---

## 目录结构

{% raw %}
Jekyll 网站的目录结构一般是：

```(txt)
.
├── _config.yml
├── _drafts
|   ├── begin-with-the-crazy-ideas.textile
|   └── on-simplicity-in-technology.markdown
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   └── post.html
├── _posts
|   ├── 2007-10-29-why-every-programmer-should-play-nethack.textile
|   └── 2009-04-26-barcamp-boston-4-roundup.textile
├── _site
├── .jekyll-metadata
└── index.html
```

具体作用:

| 文件/目录                                       | 描述                                                                                                                                                                                                                                     |
| ----------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `_config.yml`                                   | 保存配置数据                                                                                                                                                                                                                             |
| `_drafts`                                       | 保存未发布的文章，这些文件的格式中都没有`title.MARKUP`                                                                                                                                                                                   |
| `_includes`                                     | includes 可以被加载到布局或者文章中以方便重用。使用标签`{ % include file.ext %}`可以将文件`_includes/file.ext`包含进来                                                                                                                   |
| `_layouts`                                      | layouts 是包裹在文章外部的模板，layouts 可以在 YAML 头信息中根据不同的文章进行选择。标签`{{ content }}`可以将 content 插入到页面中                                                                                                       |
| `_posts`                                        | 存放发布文章的文件夹。文件格式必须符合`YEAR-MONTH-DAY-title.MARKUP`                                                                                                                                                                      |
| `_data`                                         | 存放格式化好的网站数据。jekyll 引擎会自动加载在该目录下所有的 yaml 文件（后缀是`.yal`，`.yaml`，`.json`，`.csv`）。这些文件可以通过`site.data`访问。如果有一个`members.yml`文件在该目录下，你就可以通过`site.data.members`获取文件的内容 |
| `_site`                                         | 一旦 jekyll 引擎完成转换，生成的文件就会放在这里                                                                                                                                                                                         |
| `.jekyll-metadata`                              | 该文件帮助 Jekyll 记录哪些文件从上一次建立站点开始到现在没有被修改，哪些文件需要在下一次站点建立时重新生成。                                                                                                                             |
| `index.html`和其他 HTML、Markdown、Textile 文件 | 如果这些文件中包含 YAML 头信息部分，Jekyll 就会自动将它们进行转换                                                                                                                                                                        |
| 其他文件或文件夹                                | 其他一些未被提及的目录和文件如`css`还有`images`文件家，`favicon.ico`等文件都将被完全拷贝到生成的 site 中。                                                                                                                               |

`index.html`或`index.markdown`是博客的入口。

## 查看默认主题

使用`bundle show`+主题包名称查看主题包的位置，如使用`bundle show minima`查询 Jekyll 默认主题包的位置

默认主题文件结构如下:

```(txt)
.
│  LICENSE.txt
│  README.md
│
├─assets
│      main.scss
│      minima-social-icons.svg
│
├─_includes
│      disqus_comments.html
│      footer.html
│      google-analytics.html
│      head.html
│      header.html
│      icon-github.html
│      icon-github.svg
│      icon-twitter.html
│      icon-twitter.svg
│      social.html
│
├─_layouts
│      default.html
│      home.html
│      page.html
│      post.html
│
└─_sass
    │  minima.scss
    │
    └─minima
            _base.scss
            _layout.scss
            _syntax-highlighting.scss
```

在下列文件夹中，Jekyll 会优先查看您站点中的内容，然后查看主题的默认内容（个人站点的内容会覆盖主题中的内容）：

- /assets
- /\_layouts
- /\_includes
- /\_sass

## layout

layout 文件告诉 Jekyll 如何形成一个 html 页面

以 minima 里面的`page.html`文件为例：

```(html)
---
layout: default
---
<article class="post">

  <header class="post-header">
    <h1 class="post-title">{{ page.title | escape }}</h1>
  </header>

  <div class="post-content">
    {{ content }}
  </div>

</article>
```

开头的`layout: default`说明这个文件不是最基本的 layout 文件，它依赖于`default.html`，它自己将作为 content 插入到`default.html`的`{{content}}`中。

minima 中的`default.html`:

```(html)
<!DOCTYPE html>
<html lang="{{ page.lang | default: site.lang | default: "en" }}">

  {%- include head.html -%}

  <body>

    {%- include header.html -%}

    <main class="page-content" aria-label="Content">
      <div class="wrapper">
        {{ content }}
      </div>
    </main>

    {%- include footer.html -%}

  </body>

</html>
```

在 layout 文件中使用了 Liquid 模板语言，如：

- `{{ page.lang | default: site.lang | default: "en" }}` 输出 page.lang 的值，如果不存在，则输出 site.lang 的值，如果 site.lang 不存在，则输出 en
- `{%- include head.html -%}` 将 head.html 里的内容插进来
- `{{ content }}` 引用该 layout 的文件的 content 将插入该位置

入口文件`index.markdown`:

```(markdown)
---
layout: home
---
```


`index.markdown`就是通过`layout: home`将内容插入到`home.html`中的`{{content}}`位置

## 记录一些搭建博客中看到的模板语言

## 参考

<http://jekyllcn.com/>

<https://liquid.bootcss.com/>

<https://766.js.org/2014/02/12/how-to-deploy-a-blog-on-github-by-jekyll.html>

{% endraw %}