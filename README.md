<div align="center">

# Hugo Theme Redefine

**Redefine your writing with Hugo.**

[EvanNotFound 的 hexo-theme-redefine](https://github.com/EvanNotFound/hexo-theme-redefine)（v2.9.0）的 Hugo 完整移植版

[![License: GPL-3.0](https://img.shields.io/badge/License-GPL--3.0-blue.svg)](LICENSE)
[![Hugo](https://img.shields.io/badge/Hugo-%E2%89%A5%200.146.0-ff4088.svg)](https://gohugo.io/)
[![Original Theme](https://img.shields.io/badge/Original-hexo--theme--redefine-8A2BE2.svg)](https://github.com/EvanNotFound/hexo-theme-redefine)

</div>

---

> **声明**
>
> 本主题是 [EvanNotFound](https://github.com/EvanNotFound) 的 Hexo 主题 [hexo-theme-redefine](https://github.com/EvanNotFound/hexo-theme-redefine) 的 Hugo 移植版。模板、样式、脚本与交互均移植自原项目，视觉与配置结构尽量保持一致。原项目以 **GPL-3.0** 协议开源，本移植版同样以 GPL-3.0 发布，并保留原项目的版权声明。

## 特性

- 🏠 首页 Banner（static / fixed 两种模式、打字机副标题、一言 hitokoto、社交图标与二维码抽屉）
- 🌗 明暗模式切换（跟随系统 + 手动切换 + 本地记忆，无闪烁）
- 🔍 本地搜索（`search.xml`，与 hexo-generator-searchdb 相同格式，前端搜索逻辑零改动复用）
- 📑 文章 TOC（可配置深度、自动编号、随滚动高亮）
- 💻 代码块：Hugo 内置 Chroma 服务端高亮 + 12 套原版 hljs 配色（亮色 3 套 / 暗色 9 套）、mac 风格、一键复制、折叠
- 🧩 内容短代码：`callout` / `folding` / `tabs` / `button` / `grid`，并兼容 Hexo 旧标签 `note`、`noteL`、`btn`、`cell`、`btns` 等
- ∑ 数学公式：KaTeX 构建期渲染（行内）+ 按需客户端渲染（块级），与原站 markdown-it-katex 观感一致
- 🖼️ 图片懒加载、图注、外链图标（与 Hexo 版滤镜行为一致）
- 💬 评论系统：Waline / Twikoo / Giscus / Gitalk / Utterances / Artalk
- 📄 特殊页面模板：归档、分类、标签、友链、说说（Essays）、瀑布流相册（Masonry）、书签导航（Bookmarks）、404
- 🔄 Swup 单页转场（与原版相同的插件组合）
- 🌍 多语言：en / zh-cn / zh-tw / ja / fr / es
- 📊 访问统计（Vercount/不蒜子兼容）、站点运行时间、字数与阅读时长统计
- 📝 文章推荐（基于 Hugo 内置 Related Content，替代原 nodejieba 方案）
- 🎵 APlayer、Mermaid、Pangu.js 支持

## 快速开始

```bash
# 方式一：git submodule
git submodule add https://github.com/EliorFoy/hugo-theme-redefine themes/hugo-theme-redefine

# 方式二：直接复制本主题目录到 themes/ 下
```

站点 `hugo.toml`：

```toml
theme = "hugo-theme-redefine"

[markup]
  [markup.highlight]
    codeFences = true
    noClasses = false
    lineNos = true
    lineNumbersInTable = true
  [markup.goldmark.renderer]
    unsafe = true
```

> 主题自带 [exampleSite](exampleSite/)，可直接体验：
>
> ```bash
> hugo server --source exampleSite
> ```

## 从 Hexo 迁移

- **配置**：把 `_config.redefine.yml` 的内容原样放进站点的 `config/_default/params.yaml`（键结构一致）。
- **文章**：`source/_posts` → `content/posts`；页面 `type: categories/tags` 等改用 front matter `layout: categories/tags`；数据文件 `source/_data/*.yml` → `data/*.yml`（links/essays/masonry/bookmarks）。
- **语言键**：Hugo 要求小写，`zh-CN` → `zh-cn`。
- **permalink**：建议 `posts = "/:year/:month/:day/:slugorfilename/"`，与 Hexo 的“文件名作 URL”行为一致，避免同标题文章互相覆盖。
- **数学公式**：见下文，站点配置需启用 goldmark passthrough 扩展。

## 内容写作

### 普通文章

放在 `content/posts/` 下（可用 `params.posts_section` 自定义 section 名）：

```markdown
---
title: 我的文章
date: 2026-01-01T10:00:00+08:00
description: 摘要描述
cover: /images/cover.webp     # 封面
thumbnail: /images/thumb.webp # 首页缩略图
sticky: true                   # 置顶标记
tags: [hugo]
categories: [blog]
copyright: "<a href='...'>自定义版权</a>"  # 可选，覆盖默认许可
expires: 365                   # 可选，过期提醒（天）
mathjax: true                  # 可选，启用数学公式渲染
---
```

### 特殊页面

通过 front matter `layout` 字段启用（与 Hexo 的 `type`/`template` 对应）：

| 页面 | front matter | 数据来源 |
| ---- | ------------ | -------- |
| 归档 | `layout: archive` | 自动汇总全部文章 |
| 友链 | `layout: friends` | `data/links.yml` |
| 说说 | `layout: essays` | `data/essays.yml` |
| 瀑布流 | `layout: masonry` + `outputs: ["HTML", "MasonryData"]` | `data/masonry.yml` |
| 书签 | `layout: bookmarks` | `data/bookmarks.yml` |
| 分类/标签列表页 | title 设为 `Categories` / `Tags`（或 `layout: categories` / `tags`） | 自动 |

## 短代码（与 Hexo 标签对应）

```markdown
{{</* callout info */>}}提示内容{{</* /callout */>}}
{{</* callout type="warning" title="标题" icon="fa-solid fa-lightbulb" */>}}...{{</* /callout */>}}

{{</* folding title="点我展开" open=true */>}}内容{{</* /folding */>}}

{{</* tabs demo active=1 */>}}
<!-- tab Go -->
代码
<!-- endtab -->
<!-- tab Plain -->
文字
<!-- endtab -->
{{</* /tabs */>}}

{{</* button text="GitHub" url="https://github.com" icon="fa-brands fa-github" size="lg" */>}}

{{</* grid cols=2 */>}}
{{</* button text="A" url="#" */>}}
{{</* button text="B" url="#" */>}}
{{</* /grid */>}}
```

旧版 Hexo 标签同样可用：`note`（= 简单 callout）、`notel`/`notelarge`（= 带标题 callout，标题默认 Warning）、`btn`、`cell`、`btns`、`buttons`、`subtabs`、`subsubtabs`。

> 嵌套提示：在 tabs/folding/callout 内部再嵌套短代码时，请使用 `{{%/* tabs %}}`（百分号）形态调用，Hugo 会先渲染内部短代码再传入（`{{</* %}}` 形态下嵌套短代码不会被处理）。

## 数学公式（KaTeX）

对应原站 `markdown-it-katex` + KaTeX CSS 的组合，Hugo 版使用内置 KaTeX 在**构建期**渲染（无运行时 JS、无闪动）：

1. 站点 `hugo.toml` 中启用 passthrough 扩展（markup 配置无法由主题提供默认值，必须写在站点配置）：

```toml
[markup.goldmark.extensions.passthrough]
enable = true
[markup.goldmark.extensions.passthrough.delimiters]
inline = [['$', '$'], ['\(', '\)']]
block = [['\[', '\]'], ['$$', '$$']]
```

2. 文章 front matter 中 `mathjax: true`（沿用 Hexo 习惯的键名）。
3. 行内公式 `$...$` 或 `\(...\)`，块级公式 `$$...$$` 或 `\[...\]`。

KaTeX 样式表会在页面包含公式时自动按需加载；中文/Unicode 符号已通过 `strict: ignore` 容错。注意：Hugo 内置 KaTeX 引擎输出的 HTML 使用少量改名类（`.katex-base` 等），主题自带 `css/katex-tomath.css` 适配层将其映射回官方 KaTeX CSS 规则——**请勿移除该文件**，否则分式会错位。块级公式由 KaTeX auto-render 客户端渲染（与原站注入 katex.min.js 的形态一致），Swup 切换后自动重排。

## 配置

配置结构与 Hexo 版 `_config.yml` 一致，全部位于 `[params]` 下（`params.info`、`params.colors`、`params.home_banner`……），完整默认值见主题根目录的 [hugo.toml](hugo.toml)。常用项：

```toml
[params]
date_format = "YYYY-MM-DD"   # 支持 moment 风格 token，自动转换
time_format = "HH:mm:ss"

[params.colors]
primary = "#A31F34"
default_mode = "light"

[params.navbar.links]
[params.navbar.links.Archives]
path = "/archives/"
icon = "fa-regular fa-archive"

[params.comment]
enable = true
system = "waline"   # waline / gitalk / twikoo / giscus / utterances / artalk
```

导航/侧栏链接顺序：Hugo 的 map 按字母排序，如需自定义顺序请使用数组形式：

```toml
[[params.navbar.links.list]]
name = "Archives"
path = "/archives/"
icon = "fa-regular fa-archive"
```

社交链接同时支持两种形态（与 Hexo 新旧格式兼容）：

```toml
[params.home_banner.social_links.links]
github = "https://github.com/you"      # map 形式（Hexo 旧格式）
email = "you@example.com"

# 或数组形式（可自定义顺序）
[[params.home_banner.social_links.links.list]]
name = "GitHub"
url = "https://github.com/you"
```

## 与 Hexo 版的差异

| Hexo 版功能 | Hugo 版处理方式 |
| ----------- | --------------- |
| Stylus 运行时编译 | 预编译为 `static/css/style.css`；配置驱动的部分（主色、导航渐变、宽度、字号、字体等）由模板生成 CSS 变量覆盖层（`css-overrides`） |
| highlight.js 服务端高亮 | Hugo 内置 Chroma（classes 模式）+ `chroma-adapter.css` 映射到原版 12 套 hljs 调色板 |
| hexo-generator-searchdb | 内置自定义输出格式，生成同格式 `search.xml`，前端逻辑零改动 |
| hexo-filter-mathjax / markdown-it-katex | 内置 KaTeX：行内构建期渲染 + 块级客户端 auto-render，含改名类适配层 |
| 文章推荐（nodejieba TF-IDF） | Hugo 内置 Related Content（tags/categories/keywords） |
| hexo-blog-encrypt 文章加密 | 暂未迁移（Hugo 无法在构建期做 AES；有需求可配合服务端方案） |
| hexo-all-minifier 资源压缩 | 使用 `hugo --minify` 构建即可 |
| 首页置顶排序（sticky 值） | 置顶标记已支持；排序请用 Hugo `weight` |
| 启动时版本检查（welcome 横幅） | 移除（与构建产物无关） |
| `cdn` 配置 | 预留参数但未实现 CDN 替换（Hugo 主题资源本地发布即可） |
| 语言键 `zh-CN` | Hugo 要求语言键小写：`zh-cn`、`zh-tw` |
| hexo wordcount | 内置 CJK 感知字数统计 partial |

## 目录结构

```
hugo-theme-redefine/
├── hugo.toml            # 主题默认配置（params 与 Hexo _config.yml 同构）
├── layouts/             # 模板（baseof + 布局 + partials + shortcodes + render hooks）
├── static/              # 编译好的 CSS/JS、字体、图标（与 Hexo source/ 同构）
│   ├── css/style.css    # Stylus 编译产物
│   ├── css/hljs/        # 12 套 hljs 配色
│   └── js/build/        # 原版前端 JS 构建产物（js/ 为 developer 模式未打包源码）
├── i18n/                # 模板翻译（6 语言）
├── data/redefine/i18n/  # window.i18n 客户端翻译数据
├── archetypes/
└── exampleSite/         # 示例站
```

## 致谢

- 原主题：[EvanNotFound/hexo-theme-redefine](https://github.com/EvanNotFound/hexo-theme-redefine)（GPL-3.0），本移植的全部视觉设计与前端交互均来自原项目
- [Hugo](https://gohugo.io) 与 [KaTeX](https://katex.org)、[Swup](https://swup.js.org)、[Mermaid](https://mermaid.js.org) 等开源库

## License

GPL-3.0（继承自原项目），详见 [LICENSE](LICENSE)。
