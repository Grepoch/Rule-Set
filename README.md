# Clash Rules

个人维护的 mihomo (Clash Meta) 规则集合，专注于网盘下载、社交媒体等场景的精细化分流。

## 📁 仓库结构

```
clash-rules/
├── domain/                    # 纯域名规则（高性能，可编译为 mrs）
│   ├── cloud-drive.list      # 网盘下载规则
│   ├── social-media.list     # 社交媒体规则
│   └── ai-services.list      # AI 服务规则
├── classical/                 # 混合规则（含进程名等）
│   └── README.md
├── mrs/                       # GitHub Actions 自动编译生成
│   ├── cloud-drive.mrs
│   ├── social-media.mrs
│   └── ai-services.mrs
├── .github/workflows/
│   └── compile-mrs.yml       # 自动编译 mrs
└── README.md
```

## 🚀 在 mihomo 配置中使用

### 方式一：text 格式（推荐，易调试）

```yaml
rule-providers:
  cloud-drive:
    type: http
    behavior: domain
    format: text
    url: "https://raw.githubusercontent.com/Grepoch/clash-rules/main/domain/cloud-drive.list"
    path: ./ruleset/cloud-drive.list
    proxy: DIRECT
    interval: 86400

  social-media:
    type: http
    behavior: domain
    format: text
    url: "https://raw.githubusercontent.com/Grepoch/clash-rules/main/domain/social-media.list"
    path: ./ruleset/social-media.list
    proxy: DIRECT
    interval: 86400

rules:
  - RULE-SET,cloud-drive,💾 网盘下载
  - RULE-SET,social-media,📱 社交媒体
```

### 方式二：mrs 格式（最快，二进制）

```yaml
rule-providers:
  cloud-drive:
    type: http
    behavior: domain
    format: mrs
    url: "https://raw.githubusercontent.com/Grepoch/clash-rules/main/mrs/cloud-drive.mrs"
    path: ./ruleset/cloud-drive.mrs
    proxy: DIRECT
    interval: 86400
```

### 方式三：通过 jsDelivr CDN 加速（国内访问）

把 `raw.githubusercontent.com/Grepoch/clash-rules/main` 替换为：
```
https://cdn.jsdmirror.com/gh/Grepoch/clash-rules@main
```

## 📋 规则集说明

### `domain/cloud-drive.list` — 网盘下载

覆盖以下平台的所有相关域名：

- **Google Drive / Docs / Sheets / Slides**：包括 `drivefrontend-pa.googleapis.com`、`signaler-pa.googleapis.com` 等关键 API 子域
- **Google Photos**：`photos.google.com`、`photosdata-pa.googleapis.com`
- **OneDrive / SharePoint**：`1drv.com`、`onedrive.live.com`、`sharepoint.com`
- **iCloud Drive**：`icloud.com`、`icloud-content.com`
- **Dropbox**、**MEGA**、**Box**、**MediaFire**、**4shared**、**SendSpace**、**WeTransfer**

### `domain/social-media.list` — 社交媒体

覆盖以下平台：

- **微博客**：X (Twitter)、Reddit、Threads、Tumblr、Mastodon
- **Meta 系**：Facebook、Instagram
- **即时通讯**：Telegram、Discord、WhatsApp、Signal、LINE、Viber、Skype
- **直播**：Twitch
- **职场**：LinkedIn、Slack
- **其他**：Pinterest、Snapchat、Clubhouse

### `domain/ai-services.list` — AI 服务

- ChatGPT / OpenAI、Claude / Anthropic、Gemini / Google AI、GitHub Copilot、Perplexity、Poe、Midjourney、Civitai 等

## 🔧 规则格式约定

每个 `.list` 文件只写规则内容，**不写目标策略组**（在主配置的 `rules` 里指定）。

支持的规则类型：

```
DOMAIN,example.com
DOMAIN-SUFFIX,example.com
DOMAIN-KEYWORD,keyword
IP-CIDR,1.2.3.0/24
IP-CIDR6,2001:db8::/32
PROCESS-NAME,app-name
```

## 🔄 自动更新

mihomo 会按 `interval` 定期从 URL 拉取最新规则（默认 24 小时）。修改规则后只需 `git push`，所有客户端会自动同步。

## 📝 维护

- 规则文件按域名字母顺序排列
- 用 `# === 分类 ===` 注释分组
- 添加新平台时同时更新本 README

## 📜 License

MIT
