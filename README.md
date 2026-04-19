# HapBlog

基于 [Zola](https://www.getzola.org/) 和 [austere](https://github.com/tomwrw/austere-theme-zola) 的极简纸质博客源码仓库。

## 本地开发

```bash
zola serve
```

默认地址为 `http://127.0.0.1:1111`。

## 常用命令

```bash
zola check
zola build
```

## 页面内容修改指南

这份站点的文字内容主要分成两类：

- 页面正文：放在 `content/`
- 站点公共文案：放在 `config.toml`

如果你主要是想“改页面上的文字”，优先看下面这几处。

### 1. 首页文字

文件：`content/_index.md`  
对应页面：`/`

你可以在这里修改：

- 首页主标题
- 首页介绍段落
- 首页的列表内容

当前示例：

```md
# HapBlog

这是一个以写作为核心的个人站点。
```

如果你想把首页改成个人介绍页，通常只需要直接改这个文件正文，不需要动模板。

### 2. About 页面文字

文件：`content/about.md`  
对应页面：`/about/`

你可以在这里修改：

- 页面标题 `title`
- 页面摘要 `description`
- About 正文内容

示例：

```toml
+++
title = "关于"
description = "关于 Hapexin、工作方式以及这个站点。"
+++
```

下面紧跟的 Markdown 正文就是页面显示的主要内容。

### 3. Posts 列表页文字

文件：`content/posts/_index.md`  
对应页面：`/posts/`

你可以在这里修改：

- 列表页标题
- 列表页顶部说明文字

示例：

```toml
+++
title = "Posts"
description = "较长的博客文章与系统化记录。"
+++
```

如果你想把导航里的 `Posts` 改成 `博客`，除了这个文件，还要一起修改 `config.toml` 里的导航文案。

### 4. 单篇文章文字

文件：`content/posts/*.md`  
对应页面：`/posts/<文章slug>/`

每篇文章都由一个独立 Markdown 文件控制。你通常会修改：

- 标题 `title`
- 日期 `date`
- 摘要 `description`
- 标签 `tags`
- 正文内容

最小格式示例：

```toml
+++
title = "文章标题"
date = 2026-04-13
description = "给搜索与分享卡片用的一句话摘要"
[taxonomies]
tags = ["写作", "Zola"]
+++
```

正文直接写在 front matter 下方，例如：

```md
这里是正文第一段。

- 这里可以写列表
- 也可以继续写小节
```

### 5. 项目页文字

项目页分成两部分：

- `content/projects/_index.md`
  作用：控制项目页顶部标题和简介  
  对应页面：`/projects/`
- `content/projects/projects.toml`
  作用：控制每一个项目条目的文字信息

`projects.toml` 里每个项目通常包含这些字段：

```toml
[[projects]]
title = "项目名"
description = "一句话说明项目是做什么的"
url = "https://example.com"
date = "2026"
status = "Active"
tags = ["zola", "writing"]
```

字段含义：

- `title`：项目标题
- `description`：项目简介
- `url`：项目链接
- `date`：年份或时间
- `status`：项目状态
- `tags`：项目标签

如果你只是想改项目卡片上的文本，通常只需要改 `projects.toml`。

### 6. Search 页面文字

文件：`content/search.md`  
对应页面：`/search/`

这个页面一般只需要保留标题，不需要写正文。常见改动只有：

- 页面标题 `title`

## 站点公共文案修改指南

这些文字不属于某一个页面，而是全站通用。它们主要在 `config.toml`。

### 1. 站点名称和描述

文件：`config.toml`

常改字段：

```toml
title = "HapBlog"
description = "Hapexin 的个人博客，记录写作、产品与工程实践。"
author = "Hapexin"
```

作用：

- `title`：浏览器标题、头部站点名、分享信息
- `description`：SEO 描述、搜索和分享摘要的默认值
- `author`：作者信息

### 2. 头部副标题

文件：`config.toml`

```toml
[extra]
strapline = "A quiet place for posts, notes, and experiments."
```

这个字段控制站点标题旁边那一小行说明文字。

### 3. 页脚文字

文件：`config.toml`

```toml
[extra]
footer_text = "HapBlog · 由 <a href='https://www.getzola.org/'>Zola</a> 驱动"
```

这个字段控制全站底部页脚说明。支持简单 HTML。

### 4. 导航文字

文件：`config.toml`

```toml
menu_links = [
  { url = "$BASE_URL/", name = "Home" },
  { url = "$BASE_URL/posts/", name = "Posts" },
  { url = "$BASE_URL/about/", name = "About" },
  { url = "$BASE_URL/tags/", name = "Tags" },
  { url = "$BASE_URL/search/", name = "Search" },
]
```

如果你想把英文导航改成中文，可以直接改 `name`：

```toml
menu_links = [
  { url = "$BASE_URL/", name = "首页" },
  { url = "$BASE_URL/posts/", name = "博客" },
  { url = "$BASE_URL/about/", name = "关于" },
  { url = "$BASE_URL/tags/", name = "标签" },
  { url = "$BASE_URL/search/", name = "搜索" },
]
```

## 常见文本修改场景

### 场景 1：修改首页自我介绍

改这个文件：

- `content/_index.md`

例如把：

```md
这是一个以写作为核心的个人站点。
```

改成：

```md
这是我的个人博客，主要记录产品、工程和写作笔记。
```

### 场景 2：新增一篇文章

在 `content/posts/` 里新建一个 `.md` 文件，例如：

- `content/posts/my-first-note.md`

内容可以从这个模板开始：

```toml
+++
title = "我的第一篇笔记"
date = 2026-04-14
description = "这篇文章主要介绍我想长期写什么。"
[taxonomies]
tags = ["笔记", "写作"]
+++

这里开始写正文。
```

### 场景 3：修改 About 页面

改这个文件：

- `content/about.md`

最常见的是直接改 front matter 下面的 Markdown 正文，不需要改模板。

### 场景 4：新增一个项目

改这个文件：

- `content/projects/projects.toml`

直接追加一段：

```toml
[[projects]]
title = "新项目"
description = "这是一个新的项目说明。"
url = "https://example.com"
date = "2026"
status = "Active"
tags = ["tool", "blog"]
```

### 场景 5：把导航改成中文

改这个文件：

- `config.toml`

找到 `menu_links`，把每个 `name` 改成你想显示的文案。

## 修改后如何检查

修改文字后，建议本地检查一次：

```bash
zola serve
```

然后打开这些页面确认文字是否生效：

- `/`
- `/posts/`
- `/about/`
- `/projects/`
- `/search/`

如果你改的是文章内容，再顺手点开对应文章详情页检查标题、摘要和正文。

## 内容文件一览

- `content/_index.md`：首页正文
- `content/about.md`：About 页面
- `content/posts/_index.md`：Posts 列表页说明
- `content/posts/*.md`：单篇文章
- `content/projects/_index.md`：项目页顶部说明
- `content/projects/projects.toml`：项目条目内容
- `content/search.md`：Search 页面标题
- `config.toml`：站点公共文案、导航、页脚、站点名

## GitHub Pages 发布

仓库内已提供 [.github/workflows/deploy.yml](/Users/yzx/HapBlog/.github/workflows/deploy.yml:1)，会在 `main` 分支推送后自动构建并发布到 `hapexin/hapexin.github.io`。

需要在 GitHub 仓库设置里补一个 secret：

- `PAGES_DEPLOY_TOKEN`

这个 token 需要对目标仓库 `hapexin/hapexin.github.io` 具备写权限。如果你的 GitHub 用户名不是 `hapexin`，把工作流里的 `external_repository` 改成实际的 `owner/repo`。
