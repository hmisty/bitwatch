# BitWatch — Agent Notes

## 🚀 部署

使用 **GitHub Actions** 部署到 GitHub Pages（仓库 Settings > Pages > Source 设为 **GitHub Actions**），
**不要**改为 "Deploy from a branch"。

部署 workflow：`.github/workflows/deploy.yml`

- 触发条件：推送到 `main` 分支
- 使用官方 `actions/deploy-pages@v4`（上传 artifact → 部署）
- CNAME 由 workflow 自动生成（`bitwatch.blockcoach.com`），源码中不要保留 `CNAME` 文件

### ⚠️ 首次部署的额外步骤

即使 Workflow 中配置了 `cname`，第一次部署时仍需手动在仓库 Settings > Pages 中完成：
1. **Custom domain**：填入 `bitwatch.blockcoach.com`，点击 Save
2. **Enforce HTTPS**：勾选（DNS 解析生效后会自动 Provision 证书）

此后每次推送 `main` 分支，CNAME 由 workflow 自动维护，无需再手动操作。（此坑已踩过）

## 🏗 项目结构

- `index.html` — 单页应用（SPA），所有 HTML/CSS/JS 都在一个文件内
- `.github/workflows/deploy.yml` — GitHub Pages 部署配置
- `screenshot-*.jpg` — 截图
- `favicon.png` — 网站图标
- `AGENTS.md` — 本文件，给 AI agent 的项目说明

## 🔑 关键约定

- 所有功能在 `index.html` 一个文件中实现
- 使用 Vue 3 (CDN) + TailwindCSS 4 (CDN) + Font Awesome 6
- API 提供者：Blockstream Esplora（默认）和 mempool.space，用户可在页面中切换
- 数据加密存储在 localStorage，使用 AES-GCM

## 🧪 开发

`index.html` 是单文件，修改后直接打开浏览器即可预览。
提交到 `main` 后自动触发 GitHub Actions 部署。
