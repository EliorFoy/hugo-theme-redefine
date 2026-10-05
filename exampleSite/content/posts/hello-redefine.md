---
title: "Hello Redefine"
date: 2026-09-01T10:00:00+08:00
description: "Hugo 版 Redefine 主题的第一篇文章，演示常用功能。"
tags: ["hugo", "theme"]
categories: ["blog"]
---

欢迎使用从 Hexo 完整迁移而来的 **Redefine** Hugo 主题。这篇文章演示常用写作功能。

## 代码高亮

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, Hugo Redefine!")
}
```

```javascript
const greet = (name) => `Hello, ${name}!`;
console.log(greet("Redefine"));
```

## 提示框 Callout

{{< callout info >}}
这是一个 **info** 类型的 callout，支持 Markdown。
{{< /callout >}}

{{< callout type="warning" title="带标题的提示" icon="fa-solid fa-lightbulb" >}}
命名参数用法：`type`、`title`、`icon`。
{{< /callout >}}

## 折叠块 Folding

{{< folding title="点我展开" >}}
折叠的内容支持 **Markdown** 与代码：

```python
print("inside folding")
```
{{< /folding >}}

## 多标签页 Tabs

{{< tabs demo >}}
<!-- tab Go -->
```go
fmt.Println("Go tab")
```
<!-- endtab -->
<!-- tab JavaScript -->
```javascript
console.log("JS tab");
```
<!-- endtab -->
<!-- tab Plain -->
普通文字标签页。
<!-- endtab -->
{{< /tabs >}}

## 按钮

{{< button text="GitHub" url="https://github.com" icon="fa-brands fa-github" >}}

## 网格

{{< grid cols=2 >}}
{{< button text="左侧按钮" url="#" >}}
{{< button text="右侧按钮" url="#" >}}
{{< /grid >}}

## 表格与引用

| 功能 | 状态 |
| ---- | ---- |
| 本地搜索 | ✅ |
| 暗色模式 | ✅ |
| Swup 转场 | ✅ |

> 这是一段引用文字，迁移后样式保持一致。

## 待办

- [x] 模板迁移
- [ ] 你的第一篇文章
