---
title: "Markdown 写作指南"
date: 2026-09-10T14:30:00+08:00
description: "标题层级、列表、图片、任务列表等写作元素演示。"
tags: ["markdown"]
categories: ["blog", "guide"]
---

## 二级标题

正文内容，中英文混排测试：Hugo 是最快的静态站点生成器之一。

### 三级标题

有序列表：

1. 第一步
2. 第二步
3. 第三步

无序列表：

- 支持 **加粗**、*斜体*、~~删除线~~
- 行内代码：`hugo server`
- [外部链接](https://gohugo.io) 会自动加上跳转图标

#### 四级标题

| 语法 | 效果 |
| ---- | ---- |
| `**bold**` | **bold** |
| `*italic*` | *italic* |

{{< note info >}}
旧版 Hexo 的 `{% note %}` 标签也可以使用（note/noteL 等别名均已迁移）。
{{< /note >}}

{{< notel warning 注意 >}}
这是 noteL 的等价写法，带标题的提示框。
{{< /notel >}}
