# 学术主页模板 Academic Homepage Template
[ 🇺🇸 English](./README_en.md) | 🇨🇳 中文文档

![状态](https://img.shields.io/badge/状态-可用模板-success) ![Next.js](https://img.shields.io/badge/Next.js-16-black) ![React](https://img.shields.io/badge/React-19-149eca) ![Node](https://img.shields.io/badge/Node-22.x-339933) ![部署](https://img.shields.io/badge/部署-Vercel%20%7C%20EdgeOne-blue)

这是一个中英双语主页模板，适用于个人学术主页、实验室主页、技术作品集主页与研究项目展示页。你不需要先改代码，可以先从内容文件直接开始。

## 第一次使用：按这个顺序做

1. 安装并启动项目：看 [安装指南](./docs/INSTALLATION.md)
2. 配置站点语言模式：改 [content/site.json](./content/site.json)
3. 替换个人信息与主页文案：看 [内容维护指南](./docs/CONTENT-MANAGEMENT.md)
4. 部署到线上：看 [部署指南](./docs/DEPLOYMENT.md)

## 你最需要先理解的配置

配置文件： [content/site.json](./content/site.json)

```json
{
  "i18n": {
    "mode": "bilingual",
    "primaryLocale": ""
  }
}
```

参数说明：

| 参数 | 可选值 | 作用 | 建议 |
| --- | --- | --- | --- |
| `i18n.mode` | `bilingual` / `en-only` / `zh-only` | 控制生成哪些语言路由 | 双语站用 `bilingual` |
| `i18n.primaryLocale` | `en` / `zh` / `""` | 控制首次访问时默认语言策略 | 想启用浏览器语言识别就留空 `""` |

`primaryLocale` 的规则务必看清：

- `primaryLocale: "en"`：首次访问固定英文，不做浏览器语言识别
- `primaryLocale: "zh"`：首次访问固定中文，不做浏览器语言识别
- `primaryLocale: ""`：仅在这个值留空时，首次访问才会按浏览器语言识别；识别不到时回退英文

补充逻辑：

- 系统会先读取 `locale` cookie
- 只要 cookie 已存在，就优先尊重用户上次手动选择
- 浏览器语言识别只在“无 cookie 且 `primaryLocale` 为空”时生效

## 快速开始

推荐环境：

- Node.js `22.x`
- npm（Node 22 自带）

启动命令：

```bash
nvm install
nvm use
npm ci
npm run dev
```

本地访问：

- `http://localhost:3000`

如果 `npm ci` 失败，请直接看 [安装指南](./docs/INSTALLATION.md) 里的“命令选择与常见报错”。

## 先改哪些文件

下面这些文件改完，你的网站就基本可用了：

1. [content/site.json](./content/site.json)
2. [content/profile.json](./content/profile.json)
3. [content/pages/home.json](./content/pages/home.json)
4. [content/research.json](./content/research.json)
5. [content/publications.json](./content/publications.json)
6. [content/projects.json](./content/projects.json)
7. [content/timeline.json](./content/timeline.json)
8. [content/awards.json](./content/awards.json)
9. [public/images/avatar-placeholder.svg](./public/images/avatar-placeholder.svg)
10. [public/files/sample-cv.pdf](./public/files/sample-cv.pdf)

## 环境变量怎么填

模板示例文件： [.env.example](./.env.example)

| 变量名 | 是否必填 | 用途 |
| --- | --- | --- |
| `NEXT_PUBLIC_CONTACT_EMAIL_B64` | 必填 | 联系页邮箱（Base64） |
| `NEXT_PUBLIC_CONTACT_MAILTO_SUBJECT` | 选填 | 邮件标题前缀 |
| `NEXT_PUBLIC_REPOSITORY_URL` | 选填 | 页脚仓库链接 |

邮箱转 Base64 示例：

```bash
echo -n "hi@example.com" | base64
```

## 部署方式

- 想要配置最少，优先用 Vercel：看 [部署指南](./docs/DEPLOYMENT.md)
- 想要 EdgeOne 静态导出：看 [部署指南](./docs/DEPLOYMENT.md)

这个模板已处理两条部署路径的语言入口兼容：

- 请求时跳转： [proxy.ts](./proxy.ts)
- 静态导出兜底跳转： [app/(redirects)](./app/%28redirects%29)
- EdgeOne 构建和重定向： [edgeone.json](./edgeone.json)

## 文档导航

- 安装与报错处理： [docs/INSTALLATION.md](./docs/INSTALLATION.md)
- 部署到 Vercel / EdgeOne： [docs/DEPLOYMENT.md](./docs/DEPLOYMENT.md)
- 每个内容文件怎么改： [docs/CONTENT-MANAGEMENT.md](./docs/CONTENT-MANAGEMENT.md)
- 发布前逐项检查： [docs/PUBLISH-CHECKLIST.md](./docs/PUBLISH-CHECKLIST.md)
- 可选自动化（GitHub Actions）： [docs/WORKFLOW-OPTIMIZATION.md](./docs/WORKFLOW-OPTIMIZATION.md)
- 中文维护手册： [docs/maintenance-guide.md](./docs/maintenance-guide.md)

## 发布前至少执行

```bash
npm ci
npm run lint
npm run build
```

然后按 [发布检查清单](./docs/PUBLISH-CHECKLIST.md) 逐项核对。

## License

- [MIT](./LICENSE)
