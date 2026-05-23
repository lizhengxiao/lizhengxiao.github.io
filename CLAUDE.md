# CLAUDE.md

此文件为 Claude Code (claude.ai/code) 在此仓库中工作提供指引。

## 项目概述

李政宵教授的个人学术主页，基于 Jekyll 构建，通过 GitHub Pages 部署于 `lizhengxiao.github.io`。

## 本地开发

```bash
bundle exec jekyll serve
```

`Gemfile` 中的 `github-pages` gem 提供 Jekyll 及全部插件。无构建/检查/测试流程。

## 架构

标准 Jekyll 结构：`_layouts/default.html` → `_layouts/page.html` → 四个内容页面。`_includes/` 提供 head、header、footer 和 lightbox 局部模板。`_sass/` 中的 SCSS 基于 Bourbon + Neat + Bitters，由 `css/main.scss` 引入。

### 布局链

`default.html` 依次引入 `head.html`、`header.html`、页面内容（`{{ content }}`）、`footer.html`。`page.html` 继承自 `default`，将内容包裹在 `.wrapper > .page` 容器中，并以 `page.title` 渲染 `<h1>` 标题。

### 内容页面

四个独立的 HTML 页面（均使用 `layout: page`），各自内联了 Google Analytics 和不蒜子访问量统计：

| 文件 | Permalink | 语言 |
|------|-----------|------|
| `index.html` | `/` | 中文 |
| `Homepage.html` | 默认 | 英文 |
| `cv.html` | `/cv/` | 中文 |
| `englishcv.html` | `/englishcv/` | 英文 |

相同的个人信息（单位、邮箱等）在各页面中重复出现，未抽取为 include。

### 注意事项

- Google Analytics `UA-108085250-1` 同时出现在 `_includes/head.html`、`_layouts/page.html`、`index.html` 和 `Homepage.html` 中，修改时需同步四处。
- `_includes/head.html` 中残留原始主题的 SEO 关键词（"Paul Soto..."），因 `site.description` 为空故无实际影响。
- 头像文件（`profilepicturenew.jpg`、`profilepicturenew-1.jpg`）体积过大（约 3.3MB 和 2.2MB）。
- `css/main.scss` 中引入了 `layout` 模块，但 `_sass/layout.scss` 文件不存在。
