# 维护手册（中文）

这份手册给“第一次接手这个仓库的人”使用。目标是让你快速改成自己的站，并且不踩语言配置和部署坑。

## 1. 首次接手操作顺序

1. 安装环境并启动：看 [INSTALLATION.md](./INSTALLATION.md)
2. 配置语言模式：改 [../content/site.json](../content/site.json)
3. 替换个人信息：改 [../content/profile.json](../content/profile.json)
4. 替换头像和 CV：改 [../public/images/avatar-placeholder.svg](../public/images/avatar-placeholder.svg)、[../public/files/sample-cv.pdf](../public/files/sample-cv.pdf)
5. 改首页和栏目文案：看 [../content/pages](../content/pages)
6. 改研究/成果/项目/时间线/奖项
7. 配置邮箱环境变量：看 [../.env.example](../.env.example)
8. 本地 lint + build 后再部署

## 2. 语言配置必须一次讲清楚

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

语义规则：

- `primaryLocale: "en"`：固定英文默认，不启用浏览器语言识别
- `primaryLocale: "zh"`：固定中文默认，不启用浏览器语言识别
- `primaryLocale: ""`：只有留空才启用浏览器语言识别

最终优先级：

1. 先读 `locale` cookie
2. 无 cookie 且 `primaryLocale` 为空时才看浏览器语言
3. 仍判断不出时回退英文

## 3. 内容文件怎么改

### 3.1 个人资料

文件： [../content/profile.json](../content/profile.json)

核心字段：`name`、`title`、`affiliation`、`social`、`avatar`、`cvLink`。

### 3.2 首页文案

文件： [../content/pages/home.json](../content/pages/home.json)

核心字段：`heroIntro`、`buttons`、`highlights`、`sections`。

### 3.3 研究、成果、项目

- 研究： [../content/research.json](../content/research.json)
- 成果： [../content/publications.json](../content/publications.json)
- 项目： [../content/projects.json](../content/projects.json)

### 3.4 时间线与奖项

- 时间线： [../content/timeline.json](../content/timeline.json)
- 奖项： [../content/awards.json](../content/awards.json)

### 3.5 首页动态和博客

- 动态： [../content/updates.json](../content/updates.json)
- 博客英文： [../content/blog/en](../content/blog/en)
- 博客中文： [../content/blog/zh](../content/blog/zh)

## 4. 资源替换

### 头像

- 把你的图片放到 [../public/images](../public/images)
- 然后在 [../content/profile.json](../content/profile.json) 里修改 `avatar`

### CV

- 把你的 PDF 放到 [../public/files](../public/files)
- 然后在 [../content/profile.json](../content/profile.json) 里修改 `cvLink`

## 5. 联系页配置

模板默认不依赖第三方表单。你需要设置：

- `NEXT_PUBLIC_CONTACT_EMAIL_B64`（必填）
- `NEXT_PUBLIC_CONTACT_MAILTO_SUBJECT`（可选）

示例：

```bash
echo -n "hi@example.com" | base64
```

变量文件： [../.env.example](../.env.example)

## 6. 部署建议

- 配置最省心：优先 Vercel
- 明确使用静态导出：EdgeOne Pages

部署细节见： [DEPLOYMENT.md](./DEPLOYMENT.md)

## 7. 自动化是否必需

不是必需。

- 想手工维护：忽略自动化即可
- 想自动更新首页动态和 stars：看 [WORKFLOW-OPTIMIZATION.md](./WORKFLOW-OPTIMIZATION.md)

## 8. 发布前最后检查

先执行：

```bash
npm run lint
npm run build
```

再按清单检查： [PUBLISH-CHECKLIST.md](./PUBLISH-CHECKLIST.md)

## 9. 什么时候才需要改代码

只有这些情况再改 `app/` 或 `components/`：

- 你要新增页面
- 你要改布局和导航结构
- 你要新增内容类型
- 你要接入后端表单

如果只是改文字、链接、项目、成果，优先改 `content/` 更稳定。
