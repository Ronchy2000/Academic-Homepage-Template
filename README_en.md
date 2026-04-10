# Academic Homepage Template

🇺🇸 English | [🇨🇳 中文文档](./README.md)

![Status](https://img.shields.io/badge/status-template%20ready-success) ![Next.js](https://img.shields.io/badge/Next.js-16-black) ![React](https://img.shields.io/badge/React-19-149eca) ![Node](https://img.shields.io/badge/Node-22.x-339933) ![Deploy](https://img.shields.io/badge/deploy-Vercel%20%7C%20EdgeOne-blue)

Live demo: [https://academic-homepage-template-orpin.vercel.app/](https://academic-homepage-template-orpin.vercel.app/)

This repository is a bilingual homepage template for personal academic sites, lab pages, technical portfolios, and project showcases. You can complete most customization by editing content files directly.

## Simplest Getting-Started Flow (Recommended)

1. Click `Use this template` on GitHub to create your own repository
2. Edit these files in your own repository first: [content/site.json](./content/site.json), [content/profile.json](./content/profile.json), [content/pages/home.json](./content/pages/home.json)
3. Push your updates to your own GitHub repository
4. Open Vercel, choose your repository, and deploy

Optional (only if you want local preview):

```bash
git clone <your-repository-url>
cd <your-repository-name>
npm ci
npm run dev
```

Detailed guides:

- Template and GitHub setup: [docs/GITHUB-TEMPLATE.md](./docs/GITHUB-TEMPLATE.md)
- Content editing: [docs/CONTENT-MANAGEMENT.md](./docs/CONTENT-MANAGEMENT.md)
- Deployment: [docs/DEPLOYMENT.md](./docs/DEPLOYMENT.md)

## Most Important Configuration

Config file: [content/site.json](./content/site.json)

```json
{
  "i18n": {
    "mode": "bilingual",
    "primaryLocale": ""
  }
}
```

Parameter meanings:

| Parameter | Values | Behavior | Recommendation |
| --- | --- | --- | --- |
| `i18n.mode` | `bilingual` / `en-only` / `zh-only` | Controls whether your pages are bilingual or single-language | Use `bilingual` for dual-language sites |
| `i18n.primaryLocale` | `en` / `zh` / `""` | Controls first-visit default locale policy | Keep `""` if you want browser-language detection |

Read this rule carefully:

- `primaryLocale: "en"`: first visit is fixed to English, browser-language detection is disabled
- `primaryLocale: "zh"`: first visit is fixed to Chinese, browser-language detection is disabled
- `primaryLocale: ""`: browser-language detection is enabled only in this case; unresolved detection falls back to English

Additional language selection logic:

- `locale` cookie is checked first
- if cookie exists, the user's last manual choice always wins
- browser-language detection runs only when there is no cookie and `primaryLocale` is empty

## Quick Start

Recommended runtime:

- Node.js `22.x`
- npm bundled with Node 22

```bash
nvm install
nvm use
npm ci
npm run dev
```

Open:

- `http://localhost:3000`

If `npm ci` fails, see the command-selection and troubleshooting section in [docs/INSTALLATION.md](./docs/INSTALLATION.md).

## First Files To Replace

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

## Environment Variables

Template file: [.env.example](./.env.example)

| Variable | Required | Purpose |
| --- | --- | --- |
| `NEXT_PUBLIC_CONTACT_EMAIL_B64` | Yes | Contact email in Base64 |
| `NEXT_PUBLIC_CONTACT_MAILTO_SUBJECT` | Optional | Subject prefix for generated mailto links |
| `NEXT_PUBLIC_REPOSITORY_URL` | Optional | Repository link shown in footer |

Base64 example:

```bash
echo -n "hi@example.com" | base64
```

## Deployment Paths

- Minimal configuration path: [Vercel steps](./docs/DEPLOYMENT.md)
- Static-export path on EdgeOne: [EdgeOne steps](./docs/DEPLOYMENT.md)

Language-page behavior is already handled by these files:

- automatic language-page entry during request handling: [proxy.ts](./proxy.ts)
- automatic language-page entry for static deployments: [app/(redirects)](./app/%28redirects%29)
- EdgeOne URL compatibility settings: [edgeone.json](./edgeone.json)

## Documentation Index

- Installation and troubleshooting: [docs/INSTALLATION.md](./docs/INSTALLATION.md)
- Deployment on Vercel / EdgeOne: [docs/DEPLOYMENT.md](./docs/DEPLOYMENT.md)
- GitHub and template publishing setup: [docs/GITHUB-TEMPLATE.md](./docs/GITHUB-TEMPLATE.md)
- Field-by-field content editing: [docs/CONTENT-MANAGEMENT.md](./docs/CONTENT-MANAGEMENT.md)
- Pre-publish checks: [docs/PUBLISH-CHECKLIST.md](./docs/PUBLISH-CHECKLIST.md)
- Optional GitHub Actions automation: [docs/WORKFLOW-OPTIMIZATION.md](./docs/WORKFLOW-OPTIMIZATION.md)
- Chinese maintenance manual: [docs/maintenance-guide.md](./docs/maintenance-guide.md)

## Before You Publish

```bash
npm ci
npm run lint
npm run build
```

Then validate with [Publish Checklist](./docs/PUBLISH-CHECKLIST.md).

## License

- [MIT](./LICENSE)
