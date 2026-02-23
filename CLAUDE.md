# CLAUDE.md

本文件为 Claude Code (claude.ai/code) 在此代码仓库中工作时提供指导。

## 项目概述

这是一个使用 [Hugo](https://gohugo.io/) 构建的中文个人博客网站（"Wheegoo 的空间站"）。博客内容主要涵盖技术话题、编程、设计模式和个人思考。

**网站地址：** http://www.wheegoo.com

## 技术栈

- **静态网站生成器：** Hugo（MemE 主题需要 extended 版本）
- **当前主题：** MemE (`themes/meme/`)
- **备用主题：** Jane (`themes/jane/`) - 通过 `config-jane.toml` 可用
- **内容格式：** Markdown + YAML Front Matter
- **主要语言：** 中文 (zh-CN)，支持 CJK

## 常用命令

### 构建网站
```bash
hugo                    # 构建到 public/ 目录
hugo -D                 # 构建包含草稿文章
hugo --minify           # 构建并压缩
```

### 开发服务器
```bash
hugo server             # 启动开发服务器 http://localhost:1313
hugo server -D          # 包含草稿文章
hugo server --disableFastRender
```

### 创建新内容
```bash
hugo new post/<文件名>.md    # 创建新博客文章
hugo new about/<文件名>.md   # 创建关于页面的内容
```

### 主题相关命令
MemE 主题需要 Hugo Extended 版本。如果遇到构建错误，请确保安装了 extended 版本。

## 架构说明

### 目录结构

```
myBlog/
├── content/              # 所有 markdown 内容
│   ├── post/            # 博客文章（主要内容）
│   └── about.md         # 关于页面
├── themes/              # Hugo 主题
│   ├── meme/           # 当前使用的主题 (MemE)
│   └── jane/           # 备用主题
├── static/              # 静态资源（从网站根目录提供服务）
│   ├── image/          # 按文章组织的图片
│   ├── css/            # 自定义 CSS 覆盖
│   └── js/             # 自定义 JavaScript
├── archetypes/          # 内容模板（默认 Front Matter）
├── config.toml          # 主配置文件（使用 MemE 主题）
├── config-jane.toml     # 备用配置（使用 Jane 主题）
└── public/              # 生成的网站（hugo 构建后）
```

### 配置文件

- **config.toml** - 使用 MemE 主题的主配置，包含大量自定义选项
- **config-jane.toml** - 使用 Jane 主题的备用配置（当前未激活）

要切换主题，将 config.toml 中的 `theme` 值从 `"meme"` 改为 `"jane"`。

### 内容组织

博客使用**基于分类 (categories) 的分类法**（而非基于分区 sections）。分类在文章的 Front Matter 中定义，而非通过文件夹结构。

**Front Matter 结构示例：**
```yaml
---
title: "文章标题"
date: 2024-01-01
categories: ["分类名称"]
tags: ["标签1", "标签2"]
---
```

### MemE 主题主要特性

- **四种首页布局：** `poetry`（诗意人生）、`footage`（视频片段）、`posts`（文章摘要，当前使用）、`page`（普通页面）
- **深色模式支持** 带切换开关
- **字体排版：** 使用 EB Garamond 和 Noto Serif SC 字体
- **中文优化：** CJK 语言支持、标点符号纠正、列表视图中显示生肖
- **数学公式：** 支持 KaTeX 或 MathJax（默认关闭）
- **代码高亮：** 带行号的语法高亮
- **SEO 优化：** 启用 JSON-LD、Open Graph、Twitter Cards
- **统计分析：** 使用不蒜子统计页面浏览量，Google Analytics（已配置但未启用）

## 重要设置

### 主题配置
- **首页布局：** `homeLayout = "posts"`（文章摘要视图）
- **分类方式：** `categoryBy = "categories"`（基于 Front Matter）
- **深色模式：** 已启用，默认为浅色模式

### 内容设置
- **摘要长度：** 39 字符
- **每页文章数：** 5
- **默认内容语言：** `zh`
- **文章宽度：** 39em
- **字体大小：** 18px，行高 2.5

### 固定链接结构
```
/categories/:slug/
/tags/:slug/
```

## 开发注意事项

- `content/post/` 目录中的文章是主要的博客内容
- 图片应放置在 `static/image/` 中，引用路径为 `/image/文件名.jpg`
- MemE 主题可通过 `config.toml` 中的 `[params]` 部分进行高度自定义
- 对于中文内容，确保设置 `hasCJKLanguage = true`（已配置）
- 主题支持 KaTeX 和 MathJax 数学公式（全局禁用，可在单篇文章中启用）
