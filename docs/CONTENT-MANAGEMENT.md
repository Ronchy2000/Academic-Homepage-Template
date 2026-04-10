# 内容维护指南 / Content Management Guide

[ 🇺🇸 English](#en-start) | [ 🇨🇳 中文](#zh-start)

<a id="zh-start"></a>

### 1. 先改哪些文件

建议顺序：

1. [../content/site.json](../content/site.json)
2. [../content/profile.json](../content/profile.json)
3. [../content/pages/home.json](../content/pages/home.json)
4. [../content/research.json](../content/research.json)
5. [../content/publications.json](../content/publications.json)
6. [../content/projects.json](../content/projects.json)
7. [../content/timeline.json](../content/timeline.json)
8. [../content/awards.json](../content/awards.json)
9. [../content/updates.json](../content/updates.json)
10. [../content/blog/en](../content/blog/en) 和 [../content/blog/zh](../content/blog/zh)

### 2. 语言模式

文件： [../content/site.json](../content/site.json)

```json
{
  "i18n": {
    "mode": "bilingual",
    "primaryLocale": ""
  }
}
```

规则：

- `mode`：`bilingual`、`en-only`、`zh-only`
- `primaryLocale: "en"`：固定英文默认
- `primaryLocale: "zh"`：固定中文默认
- `primaryLocale: ""`：仅留空时启用浏览器语言识别

### 3. 个人资料

文件： [../content/profile.json](../content/profile.json)

常改字段：

- `name`
- `title`
- `affiliation`
- `social`
- `avatar`
- `cvLink`

资源文件目录：

- [../public/images](../public/images)
- [../public/files](../public/files)

### 4. 页面文案

目录： [../content/pages](../content/pages)

常用文件：

- [../content/pages/home.json](../content/pages/home.json)
- [../content/pages/blog.json](../content/pages/blog.json)
- [../content/pages/contact.json](../content/pages/contact.json)
- [../content/pages/projects.json](../content/pages/projects.json)
- [../content/pages/publications.json](../content/pages/publications.json)
- [../content/pages/research.json](../content/pages/research.json)

### 5. 研究、成果、项目

- 研究： [../content/research.json](../content/research.json)
- 成果： [../content/publications.json](../content/publications.json)
- 项目： [../content/projects.json](../content/projects.json)

### 6. 时间线与奖项

- 时间线： [../content/timeline.json](../content/timeline.json)
- 奖项： [../content/awards.json](../content/awards.json)

### 7. Recent Updates 和博客

- 首页动态： [../content/updates.json](../content/updates.json)
- 博客英文： [../content/blog/en](../content/blog/en)
- 博客中文： [../content/blog/zh](../content/blog/zh)

自动化更新说明： [WORKFLOW-OPTIMIZATION.md](./WORKFLOW-OPTIMIZATION.md)

### 8. 单语模式维护

`en-only`：可以只保留英文内容和英文博客目录。  
`zh-only`：可以只保留中文内容和中文博客目录。

### 9. 发布前

```bash
npm run lint
npm run build
```

然后看： [PUBLISH-CHECKLIST.md](./PUBLISH-CHECKLIST.md)

---

<a id="en-start"></a>

### 1. Files to edit first

Recommended order:

1. [../content/site.json](../content/site.json)
2. [../content/profile.json](../content/profile.json)
3. [../content/pages/home.json](../content/pages/home.json)
4. [../content/research.json](../content/research.json)
5. [../content/publications.json](../content/publications.json)
6. [../content/projects.json](../content/projects.json)
7. [../content/timeline.json](../content/timeline.json)
8. [../content/awards.json](../content/awards.json)
9. [../content/updates.json](../content/updates.json)
10. [../content/blog/en](../content/blog/en) and [../content/blog/zh](../content/blog/zh)

### 2. Locale mode

File: [../content/site.json](../content/site.json)

```json
{
  "i18n": {
    "mode": "bilingual",
    "primaryLocale": ""
  }
}
```

Rules:

- `mode`: `bilingual`, `en-only`, `zh-only`
- `primaryLocale: "en"`: fixed English default
- `primaryLocale: "zh"`: fixed Chinese default
- `primaryLocale: ""`: browser-language detection runs only when empty

### 3. Profile data

File: [../content/profile.json](../content/profile.json)

Common fields:

- `name`
- `title`
- `affiliation`
- `social`
- `avatar`
- `cvLink`

Asset folders:

- [../public/images](../public/images)
- [../public/files](../public/files)

### 4. Page copy

Directory: [../content/pages](../content/pages)

Common files:

- [../content/pages/home.json](../content/pages/home.json)
- [../content/pages/blog.json](../content/pages/blog.json)
- [../content/pages/contact.json](../content/pages/contact.json)
- [../content/pages/projects.json](../content/pages/projects.json)
- [../content/pages/publications.json](../content/pages/publications.json)
- [../content/pages/research.json](../content/pages/research.json)

### 5. Research, publications, projects

- Research: [../content/research.json](../content/research.json)
- Publications: [../content/publications.json](../content/publications.json)
- Projects: [../content/projects.json](../content/projects.json)

### 6. Timeline and awards

- Timeline: [../content/timeline.json](../content/timeline.json)
- Awards: [../content/awards.json](../content/awards.json)

### 7. Recent updates and blog

- Updates: [../content/updates.json](../content/updates.json)
- English blog: [../content/blog/en](../content/blog/en)
- Chinese blog: [../content/blog/zh](../content/blog/zh)

Automation details: [WORKFLOW-OPTIMIZATION.md](./WORKFLOW-OPTIMIZATION.md)

### 8. Single-language maintenance

`en-only`: keep English content only.  
`zh-only`: keep Chinese content only.

### 9. Before release

```bash
npm run lint
npm run build
```

Then check [PUBLISH-CHECKLIST.md](./PUBLISH-CHECKLIST.md).
