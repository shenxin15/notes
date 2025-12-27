这是一个为你准备的 `README.md` 文件。它是根据你提供的视频内容（Source -）以及 GitHub 文件结构（Source）整理而成的。

你可以直接复制以下内容，保存为 `README.md` 并上传到你的 GitHub 仓库。

***

```markdown
# Zero-Cost Secure Cloud Notes (零成本安全云笔记)

这是一个基于 Cloudflare 全家桶（Workers, D1, Pages, AI）构建的零成本、端到端加密的私人云笔记应用。它支持多端同步（PWA）、阅后即焚分享以及 AI 智能总结功能。

> **灵感来源**: 本项目基于 YouTube 频道“三十槽”的视频教程《零成本！用Cloudflare自建私人笔记App，黑客也打不开》构建。

## ✨ 主要功能

*   **完全免费**: 利用 Cloudflare 免费额度（每天 500 万次数据库读取），个人使用完全足够。
*   **端到端加密**: 笔记在本地加密后上传，服务器端（包括 Cloudflare 工程师）看到的只有乱码，确保绝对隐私。
*   **阅后即焚**: 生成分享链接，对方查看一次后数据立即物理销毁。
*   **AI 智能总结**: 集成 Workers AI (Llama 模型)，可对长笔记进行智能总结。
*   **多端同步**: 支持 PWA，手机端可像原生 App 一样安装使用，体验流畅。

## 📂 文件结构

确保你的仓库包含以下核心文件：

*   `SQL.sql`: D1 数据库初始化表结构的语句。
*   `Worker.js`: 后端逻辑代码（运行在 Cloudflare Workers）。
*   `index.html`: 前端网页入口。
*   `manifest.json`: PWA 配置文件。
*   `sw.js`: Service Worker 脚本（用于 PWA 离线缓存等）。
*   `icon.png`: 应用图标。

## 🚀 部署指南

### 第一步：配置后端 (Cloudflare D1 & Workers)

1.  **创建数据库**:
    *   登录 Cloudflare -> 存储与数据库 -> D1 -> 创建数据库（建议命名为 `my-notes`）。
    *   进入数据库控制台，复制 `SQL.sql` 中的内容并执行，创建 `notes` 表。

2.  **创建 Worker**:
    *   计算和 AI -> Workers 和 Pages -> 创建应用程序 -> 创建 Worker (Hello World)。
    *   命名建议：`notes-api`。

3.  **绑定资源 (Settings -> Variables)**:
    *   **D1 数据库绑定**: 变量名填写 `DB` (大写)，选择刚才创建的数据库。
    *   **Workers AI 绑定**: 变量名填写 `AI` (大写)。
    *   **环境变量 (Secrets)**: 添加变量名 `ADMIN_KEY`，值为你设定的后端通信密码（如：`YourName666`）。

4.  **部署代码**:
    *   点击“编辑代码”，清空原有代码，将 `Worker.js` 的内容复制进去并部署。
    *   (可选建议) 在设置 -> 域和路由中添加自定义域（如 `api-notes.yourdomain.com`）以提高稳定性。

### 第二步：部署前端 (Cloudflare Pages)

1.  **上传代码**: 将本项目 fork 或上传到你的 GitHub 仓库。
2.  **创建 Pages**:
    *   Cloudflare -> Workers 和 Pages -> 创建 -> Pages -> 连接到 Git。
    *   选择本项目仓库，构建设置保持默认（留空）即可。
3.  **自定义域名**: 部署完成后，建议设置自定义域名（如 `notes.yourdomain.com`）。

### 第三步：初始化设置

1.  浏览器访问你的前端 Pages 域名。
2.  首次进入会提示配置：
    *   **Workers 链接**: 填入你的后端地址 (必须带 `https://`，例如 `https://api-notes.yourdomain.com`)。
    *   **密钥**: 填入你在 Worker 环境变量中设置的 `ADMIN_KEY`。
3.  保存后即可开始使用。

## 📖 使用说明

*   **加密存储**: 建议设置一个主密码用于所有笔记的加密，内容在本地加密后才会上传。
*   **分享笔记**: 点击“生成阅后即焚链接”，生成的 URL 包含 `public_id`，访问一次后即失效。
*   **找回笔记**: 如果更换设备或刷新缓存，需在主页输入之前的“解密密码”并刷新列表，才能解密查看云端数据。
*   **手机安装**: 在手机浏览器打开网页，点击菜单中的“添加到主屏幕”即可作为 App 使用。

## ⚠️ 免责声明

本项目仅供学习和个人使用。虽然采用了端到端加密，但请妥善保管你的 `ADMIN_KEY` 和笔记解密密码。密码丢失将导致无法找回笔记内容。

---
*Created with ❤️ based on open source sharing.*
```

### 补充建议：

根据源文件列表（Source），你的仓库中似乎包含 `icon.png` 和 `SQL.sql` 等文件。在上传到 GitHub 时，请确保：

1.  **文件完整性**：视频强调 `index.html`, `manifest.json`, `sw.js` 这三个文件对于实现 PWA（手机端像 App 一样运行）至关重要，**一个都不能漏**。
2.  **区分代码**：`Worker.js` 是放在 Cloudflare 后台运行的，不需要通过 Pages 部署，但通常为了版本管理，我们会把它也放在 GitHub 仓库里备份（如上述 README 所述）。在部署 Pages 时，Cloudflare 只会托管静态 HTML 文件，不会运行仓库里的 `Worker.js`，这一点已经在“部署指南”中区分开了。
