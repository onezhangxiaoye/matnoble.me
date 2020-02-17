+++
title = "Shortcodes 实践教程"
date = "2020-02-16T00:22:42+00:00"
description = "Hugo 这个功能太强大了"
categories = ["TECH","建站那些事儿"]
tags = ["Hugo"]
keywords = ["Shortcodes","Hugo","建站那些事儿","year","hugo-notice","music","video","friend link","gallery slider","google maps"]
toc = true
+++

## Year
官网例子, 输出今年的年份.
```
今年是 {{ < year > }} 年.
```

今年是 {{< year >}} 年.

## Hugo-notice
### Warning
```
{{ < notice warning > }}
这是告诫! 请注意!
{{ < /notice > }}
```
{{< notice warning >}}
这是告诫! 请注意!
{{< /notice >}}

### Info
```

{{ < notice info > }}
这是引言
{{ < /notice > }}
```
{{< notice info >}}
这是引言
{{< /notice >}}

### Tip

```
{{ < notice tip > }}
这是小贴示
{{ < /notice > }}
```

{{< notice tip >}}
这是小贴示
{{< /notice >}}

### Note

```
{{ < notice note > }}
这是注释
{{ < /notice > }}
```

{{< notice note >}}
这是注释
{{< /notice >}}

## Music

```
{{ < music id="569200212" type="song" server="netease" > }}
```

{{< music id="569200212" type="song" server="netease" >}}

## Video
### YouTube

```
{{ < youtube MHsiF9avPww > }}
```

{{< youtube MHsiF9avPww >}}

### YOUKU

{{< youku id="XNDU0OTY4OTg4OA==" >}}

## Friend link
```
{{ < friend name="数学小兵儿" url="https://matnoble.me/" logo="/icons/android-chrome-512x512.png" word="数学＆计算机 我都爱" > }}
```

{{< friend name="数学小兵儿" url="https://matnoble.me/" logo="/icons/android-chrome-512x512.png" word="数学＆计算机 我都爱" >}}
