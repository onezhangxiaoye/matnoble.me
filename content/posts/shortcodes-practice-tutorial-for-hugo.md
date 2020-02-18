+++
title = "Shortcodes 实践教程"
date = "2020-02-16T00:22:42+00:00"
description = "Hugo 这个功能太强大了"
categories = ["TECH","建站那些事儿"]
tags = ["Hugo"]
keywords = ["Shortcodes","Hugo","建站那些事儿","year","hugo-notice","music","video","friend link","优酷","维基百科 Wikipedia","blockquote"]
toc = true
katex = true
+++

## 前言

Shortcodes 翻译为: 短代码或者简码

{{< blockquote author="HUGO" link="https://s0gohugo0io.icopy.site/content-management/shortcodes/#what-a-shortcode-is" title="什么是简码" >}}
简码是内容文件中的一个简单片段，Hugo将使用预定义的模板对其进行呈现.

除了更清洁的Markdown外，短代码还可以随时更新以反映新的类，技术或标准. 在网站生成时，Hugo简码将轻松合并到您的更改中. 您避免了可能复杂的搜索和替换操作.
{{< /blockquote >}}

### 需注意

#### 主题适应

本博客基于 HUGO, 使用的是 [reuixiy](https://io-oi.me/) 开发的 [MemE 主题](https://github.com/reuixiy/hugo-theme-meme/), 但由于该主题暂时不支持 Shortcodes (与$\LaTeX$ 渲染冲突), 所以, 如果你用的也是该主题, 又想玩玩儿 Shortcodes, 那么你需要作出一些小修改, 修改办法见下方链接.

{{< blockquote author="reuixiy" link="https://github.com/reuixiy/hugo-theme-meme/issues/50">}}
MemE v4.0.0 breaks Hugo shortcodes
{{< /blockquote >}}

#### 代码呈现

{{< notice tip >}}
由于渲染问题, 下文中出现的
```
{{空格< sth >空格}}
```
「空格」是没有的!
{{< /notice >}}
## Shortcodes 实例
### 当前年 Year
官网例子, 输出今年的年份.
```
今年是 {{ < year > }} 年.
```
今年是 {{< year >}} 年.

只需建立 `./layouts/shortcodes/year.html`
```html
{{ now.Format "2006" }}
```

### GitHub gist
原生支持, 添加 GitHub gist
```
{{ < gist MatNoble b8d6a9541221fef7c30bf214d3505836 > }}
```
{{< gist MatNoble b8d6a9541221fef7c30bf214d3505836 >}}

### Hugo-notice
{{< blockquote author="martignoni" link="https://github.com/martignoni/hugo-notice" title="hugo-notice" >}}
This is not a standalone theme. It is a Hugo theme component providing a shortcode: notice to display nice notices. Four notice types are provided: warning, info, note and tip.
{{< /blockquote >}}
`hugo-notice` 是一个制作十分精美的短代码, 非常感谢原作者的付出, 但使用并不需要把他的仓库 copy 到本地, 只需将 `notice.html` copy 到 `./layouts/shortcodes/` 下, 如需要翻译, 且使用 `MemE 主题`, 只需要在根目录下创建 `./i18n/zh-cn.yaml`
```yaml
- id: warning
  translation: "警告"
- id: note
  translation: "注释"
- id: info
  translation: "引言"
- id: tip
  translation: "小贴示"
```
显示效果如下:
#### Warning
```
{{ < notice warning > }}
这是告诫! 请注意!
{{ < /notice > }}
```
{{< notice warning >}}
这是告诫! 请注意!
{{< /notice >}}

#### Info
```

{{ < notice info > }}
这是引言
{{ < /notice > }}
```
{{< notice info >}}
这是引言
{{< /notice >}}

#### Tip

```
{{ < notice tip > }}
这是小贴示
{{ < /notice > }}
```

{{< notice tip >}}
这是小贴示
{{< /notice >}}

#### Note

```
{{ < notice note > }}
这是注释
{{ < /notice > }}
```

{{< notice note >}}
这是注释
{{< /notice >}}

### blockquote

借鉴自[GitHub](https://github.com/parsiya/Hugo-Shortcodes/blob/master/shortcodes/blockquote.html), 举个栗子:

```
{{ < blockquote author="李健" link="https://baike.baidu.com/item/%E6%87%82%E5%BE%97/22699721" title="《懂得》" > }}
花开花谢 白天黑夜<br />
一切自然 又不尽然<br />
春夏秋冬 经过才懂<br />
世间冷暖 无非自然
{{ < /blockquote > }}
```
{{< blockquote author="李健" link="https://baike.baidu.com/item/%E6%87%82%E5%BE%97/22699721" title="《懂得》" >}}
花开花谢 白天黑夜<br />
一切自然 又不尽然<br />
春夏秋冬 经过才懂<br />
世间冷暖 无非自然
{{< /blockquote >}}

### 维基百科 Wikipedia
借鉴自[GitHub](https://github.com/parsiya/Hugo-Shortcodes/blob/master/shortcodes/wp.html), 举个栗子:
```
{{ < wp tag="Wikipedia:历史上的今天" lang="zh" title="历史上的今天" > }}
```

{{< wp tag="Wikipedia:历史上的今天" lang="zh" title="历史上的今天" >}}

### 音乐 Music
基于 [MetingJS](https://github.com/metowolf/MetingJS) 制作 `./layouts/shortcodes/music.html`
```
{{ < music id="569200212" type="song" server="netease" > }}
```
|option |  default |  description|
|:--:|:--:|:--:|
|id |  require |  song id / playlist id / album id / search keyword|
|server | require  | music platform: netease, tencent, kugou, xiami, baidu|
|type | require | song, playlist, album, search, artist|

更多选项看[这里](https://github.com/metowolf/MetingJS#option)

{{< notice warning >}}
该 shortcodes 存在问题! 会导致 TOC 目录点击失效, 所以, 暂时只能将音乐放到没有目录的页面, 比如[这里](https://matnoble.me/about/)
{{< /notice >}}

### 视频 Video
#### YouTube
原生支持 YouTube, 代码如下

```
{{ < youtube ID > }}
```

{{< youtube MHsiF9avPww >}}

#### 优酷 YOUKU
还可以创建`./layouts/shortcodes/youku.html` 使其支持 `YOUKU`
```
{{ < youku id="ID" > }}
```

{{< youku id="XNDU0OTY4OTg4OA==" >}}

### 好友链接 Friend link
很多博客都支持添加 `友链`, 本博客也不例外, 在[这里](https://matnoble.me/search/#%E5%8F%8B%E9%93%BE)
借鉴自 [hugo-friendlinks](https://github.com/kkkgo/hugo-friendlinks), 针对本主题, 稍加修改.

```
{{ < friend name="数学小兵儿" url="https://matnoble.me/" logo="/icons/android-chrome-512x512.png" word="数学＆计算机 我都爱" > }}
```

{{< friend name="数学小兵儿" url="https://matnoble.me/" logo="/icons/android-chrome-512x512.png" word="数学＆计算机 我都爱" >}}

### 提供下载 download

以上所有 `shortcodes` 代码都可以访问以下 `GitHub` 链接下载.

{{< blockquote author="数学小兵儿" link="https://github.com/MatNoble/hugo-shortcodes-sets" >}}
These are shortcodes that I have created for the Hugo static blogging engine.
{{< /blockquote >}}

### 更多示例
1. <a href="https://github.com/spf13/spf13.com/tree/master/layouts/shortcodes" title="See more examples of shortcodes by visiting the shortcode directory of the source for spf13.com, the blog of Hugo's creator, Steve Francia.">shortcodes directory for spf13.com</a>
2. <a href="https://github.com/gohugoio/hugo/tree/master/docs/layouts/shortcodes" title="See the shortcode source directory for the documentation site you're currently reading.">shortcodes directory for the Hugo docs</a>
