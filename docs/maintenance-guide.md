# 维护手册 / Maintenance Guide

[ 🇺🇸 English](#en-start) | [ 🇨🇳 中文](#zh-start)

<a id="zh-start"></a>

这份文档给第一次接手仓库的用户使用。内容按实际操作顺序写，直接照做即可。

### 1. 首次接手操作顺序

1. 安装并启动项目：看 [INSTALLATION.md](./INSTALLATION.md)
2. 先改语言配置：看 [../content/site.json](../content/site.json)
3. 替换个人资料：看 [../content/profile.json](../content/profile.json)
4. 替换头像和 CV：看 [../public/images/avatar-placeholder.svg](../public/images/avatar-placeholder.svg) 和 [../public/files/sample-cv.pdf](../public/files/sample-cv.pdf)
5. 修改页面文案：看 [../content/pages](../content/pages)
6. 修改研究、成果、项目、时间线、奖项
7. 配置环境变量：看 [../.env.example](../.env.example)
8. 本地执行 `npm run lint` 和 `npm run build`，通过后再部署

### 2. 语言配置必须一次讲清楚

文件： [../content/site.json](../content/site.json)

默认配置：

```json
{
  "i18n": {
    "mode": "bilingual",
    "primaryLocale": ""
  }
}
```

参数说明：

- `mode`：`bilingual`、`en-only`、`zh-only`
- `primaryLocale`：`en`、`zh`、`""`

`primaryLocale` 的行为规则：

- `primaryLocale: "en"`：首次访问固定英文，不启用浏览器语言识别
- `primaryLocale: "zh"`：首次访问固定中文，不启用浏览器语言识别
- `primaryLocale: ""`：仅在留空时，首次访问才启用浏览器语言识别

语言判定优先级：

1. 先读取 `locale` cookie
2. 无 cookie 且 `primaryLocale` 为空时，读取浏览器语言
3. 仍无法判断时回退英文

### 3. 内容文件怎么改

优先改这些文件：

- 站点配置： [../content/site.json](../content/site.json)
- 个人资料： [../content/profile.json](../content/profile.json)
- 首页文案： [../content/pages/home.json](../content/pages/home.json)
- 研究： [../content/research.json](../content/research.json)
- 成果： [../content/publications.json](../content/publications.json)
- 项目： [../content/projects.json](../content/projects.json)
- 时间线： [../content/timeline.json](../content/timeline.json)
- 奖项： [../content/awards.json](../content/awards.json)
- 首页动态： [../content/updates.json](../content/updates.json)
- 博客： [../content/blog/en](../content/blog/en) 和 [../content/blog/zh](../content/blog/zh)

如果只是修改标题、按钮、描述、列表内容，优先改 `content` 目录，不要先改组件代码。

### 4. 资源与环境变量

头像和 CV：

- 把头像放到 [../public/images](../public/images)
- 把 CV 放到 [../public/files](../public/files)
- 在 [../content/profile.json](../content/profile.json) 中同步修改 `avatar` 和 `cvLink`

联系页变量：

- 必填：`NEXT_PUBLIC_CONTACT_EMAIL_B64`
- 可选：`NEXT_PUBLIC_CONTACT_MAILTO_SUBJECT`

示例：

```bash
echo -n "hi@example.com" | base64
```

### 5. 部署建议

- 想要最省事：优先 Vercel
- 明确要静态导出：EdgeOne Pages

部署细节看： [DEPLOYMENT.md](./DEPLOYMENT.md)

### 6. 自动化是否需要

不是必需。

- 想手工维护：不启用自动化
- 想自动更新首页动态和 stars：看 [WORKFLOW-OPTIMIZATION.md](./WORKFLOW-OPTIMIZATION.md)

### 7. 发布前检查

先执行：

```bash
npm run lint
npm run build
```

再逐项检查： [PUBLISH-CHECKLIST.md](./PUBLISH-CHECKLIST.md)

GitHub 与 Template 发布设置： [GITHUB-TEMPLATE.md](./GITHUB-TEMPLATE.md)

### 8. 什么时候才需要改代码

只有以下情况建议改 `app` 或 `components`：

- 你要新增页面
- 你要改布局和导航结构
- 你要新增内容类型
- 你要接入后端表单

如果只是改文案、链接、项目、成果，保持 `content` 驱动即可。

---

<a id="en-start"></a>

This guide is for first-time users of the repository. Follow the steps in order.

### 1. First-time handover sequence

1. Install and run locally: [INSTALLATION.md](./INSTALLATION.md)
2. Configure locale mode first: [../content/site.json](../content/site.json)
3. Replace profile data: [../content/profile.json](../content/profile.json)
4. Replace avatar and CV: [../public/images/avatar-placeholder.svg](../public/images/avatar-placeholder.svg) and [../public/files/sample-cv.pdf](../public/files/sample-cv.pdf)
5. Update page copy: [../content/pages](../content/pages)
6. Update research, publications, projects, timeline, and awards
7. Configure environment variables: [../.env.example](../.env.example)
8. Run `npm run lint` and `npm run build` before deployment

### 2. Locale configuration (must be clear)

File: [../content/site.json](../content/site.json)

Default:

```json
{
  "i18n": {
    "mode": "bilingual",
    "primaryLocale": ""
  }
}
```

Parameters:

- `mode`: `bilingual`, `en-only`, `zh-only`
- `primaryLocale`: `en`, `zh`, `""`

`primaryLocale` behavior:

- `primaryLocale: "en"`: first visit is fixed to English, browser-language detection is disabled
- `primaryLocale: "zh"`: first visit is fixed to Chinese, browser-language detection is disabled
- `primaryLocale: ""`: browser-language detection runs only when this value is empty

Locale decision order:

1. Read `locale` cookie first
2. If no cookie and `primaryLocale` is empty, read browser language
3. Fall back to English if still undecidable

### 3. How to edit content files

Edit these files first:

- Site config: [../content/site.json](../content/site.json)
- Profile: [../content/profile.json](../content/profile.json)
- Home copy: [../content/pages/home.json](../content/pages/home.json)
- Research: [../content/research.json](../content/research.json)
- Publications: [../content/publications.json](../content/publications.json)
- Projects: [../content/projects.json](../content/projects.json)
- Timeline: [../content/timeline.json](../content/timeline.json)
- Awards: [../content/awards.json](../content/awards.json)
- Recent updates: [../content/updates.json](../content/updates.json)
- Blog: [../content/blog/en](../content/blog/en) and [../content/blog/zh](../content/blog/zh)

If your change is only text or links, edit `content` files first, not component code.

### 4. Assets and environment variables

Avatar and CV:

- Put avatar files in [../public/images](../public/images)
- Put CV files in [../public/files](../public/files)
- Update `avatar` and `cvLink` in [../content/profile.json](../content/profile.json)

Contact page variables:

- Required: `NEXT_PUBLIC_CONTACT_EMAIL_B64`
- Optional: `NEXT_PUBLIC_CONTACT_MAILTO_SUBJECT`

Example:

```bash
echo -n "hi@example.com" | base64
```

### 5. Deployment choice

- Use Vercel for the simplest setup
- Use EdgeOne Pages if you need static export deployment

See [DEPLOYMENT.md](./DEPLOYMENT.md).

### 6. Is automation required?

No.

- Use manual updates if you want full control
- Use automation for recent updates and stars: [WORKFLOW-OPTIMIZATION.md](./WORKFLOW-OPTIMIZATION.md)

### 7. Pre-release checks

Run:

```bash
npm run lint
npm run build
```

Then follow [PUBLISH-CHECKLIST.md](./PUBLISH-CHECKLIST.md).

GitHub and template publishing setup: [GITHUB-TEMPLATE.md](./GITHUB-TEMPLATE.md)

### 8. When should you edit code?

Edit `app` or `components` only when:

- you need a new page
- you need to change layout or navigation
- you need a new content type
- you need backend form integration

For content-only updates, keep using the `content` directory.
