# Content Management Guide / 内容维护指南

这份文档按“用户如何改内容”来组织。你可以不改 TSX 代码，先把站点改到可上线状态。

## 1. 推荐修改顺序

1. [../content/site.json](../content/site.json)
2. [../content/profile.json](../content/profile.json)
3. [../content/pages/home.json](../content/pages/home.json)
4. [../content/research.json](../content/research.json)
5. [../content/publications.json](../content/publications.json)
6. [../content/projects.json](../content/projects.json)
7. [../content/timeline.json](../content/timeline.json)
8. [../content/awards.json](../content/awards.json)
9. [../content/updates.json](../content/updates.json)
10. [../content/blog/en](../content/blog/en) 或 [../content/blog/zh](../content/blog/zh)
11. [../public/images/avatar-placeholder.svg](../public/images/avatar-placeholder.svg)
12. [../public/files/sample-cv.pdf](../public/files/sample-cv.pdf)

## 2. 站点语言模式（最关键）

文件： [../content/site.json](../content/site.json)

```json
{
  "i18n": {
    "mode": "bilingual",
    "primaryLocale": ""
  }
}
```

### 2.1 `i18n.mode` 可选值

- `bilingual`：生成 `/en/*` 和 `/zh/*`
- `en-only`：只生成 `/en/*`
- `zh-only`：只生成 `/zh/*`

### 2.2 `i18n.primaryLocale` 行为规则

- `"en"`：首次访问固定英文，不启用浏览器语言识别
- `"zh"`：首次访问固定中文，不启用浏览器语言识别
- `""`：只有留空才启用浏览器语言识别；识别不到回退英文

### 2.3 实际优先级

1. 先读 `locale` cookie
2. 无 cookie 且 `primaryLocale` 为空时，才读浏览器语言
3. 无法判断时回退英文

## 3. 个人信息

文件： [../content/profile.json](../content/profile.json)

常用字段：

- `name`
- `nativeName`
- `aka`
- `title`
- `affiliation`
- `location`
- `keywords`
- `social`（数组，元素为 `{ label, href }`）
- `avatar`
- `cvLink`

配套资源：

- 头像文件放到 [../public/images](../public/images)
- CV 文件放到 [../public/files](../public/files)

示例：

```json
{
  "avatar": "/images/my-photo.jpg",
  "cvLink": "/files/my-cv.pdf"
}
```

## 4. 页面文案

目录： [../content/pages](../content/pages)

常改文件：

- 首页： [../content/pages/home.json](../content/pages/home.json)
- 博客页： [../content/pages/blog.json](../content/pages/blog.json)
- 联系页： [../content/pages/contact.json](../content/pages/contact.json)
- 项目页： [../content/pages/projects.json](../content/pages/projects.json)
- 成果页： [../content/pages/publications.json](../content/pages/publications.json)
- 研究页： [../content/pages/research.json](../content/pages/research.json)

你要改标题、按钮、说明文案，优先改这里，不要先改组件。

## 5. 研究、成果、项目

### 5.1 研究页

文件： [../content/research.json](../content/research.json)

- `interests`：研究兴趣卡片
- `experiences`：研究经历（`title`、`period`、`summary`、`bullets` 等）

### 5.2 成果页

文件： [../content/publications.json](../content/publications.json)

条目类型：

- `C` 会议
- `J` 期刊
- `P` 专利
- `S` 投稿/在审

建议每条统一填写：`id`、`title`、`authors`、`venue`、`year`、`links`。

### 5.3 项目页

文件： [../content/projects.json](../content/projects.json)

- 分组：`academic`、`open-source`
- 条目常用字段：`name`、`summary`、`period`、`role`、`tags`、`links`、`metrics`

## 6. 时间线与奖项

- 时间线： [../content/timeline.json](../content/timeline.json)
- 奖项： [../content/awards.json](../content/awards.json)

时间线建议把 `education` 与 `experience` 各控制在 2-5 条，便于阅读。

## 7. 首页 Recent Updates

文件： [../content/updates.json](../content/updates.json)

两种维护方式：

1. 手动维护
2. 用 GitHub Actions 自动覆盖

自动化说明见： [./WORKFLOW-OPTIMIZATION.md](./WORKFLOW-OPTIMIZATION.md)

## 8. 博客内容

目录：

- 英文： [../content/blog/en](../content/blog/en)
- 中文： [../content/blog/zh](../content/blog/zh)

路由规则：文件名就是 slug。  
示例：`content/blog/en/my-first-post.mdx` -> `/en/blog/my-first-post`

推荐 frontmatter：

```yaml
---
title: "My First Post"
date: "2026-04-10"
summary: "One-line summary shown in the blog list."
tags: ["Notes"]
type: "note"
draft: false
---
```

数学公式支持 KaTeX：

```md
Inline: $E = mc^2$

Block:
$$
\nabla \cdot \mathbf{E} = \rho / \varepsilon_0
$$
```

## 9. 单语站如何简化维护

如果 `mode` 为 `en-only`：

- 可只保留 `en` 内容块
- 可只保留 [../content/blog/en](../content/blog/en)

如果 `mode` 为 `zh-only`：

- 可只保留 `zh` 内容块
- 可只保留 [../content/blog/zh](../content/blog/zh)

## 10. 发布前检查

```bash
npm run lint
npm run build
```

再全文搜索这些占位词：

- `your-handle`
- `example.com`
- `Example University`
- `YOUR_ID`

完整发布清单见： [./PUBLISH-CHECKLIST.md](./PUBLISH-CHECKLIST.md)
