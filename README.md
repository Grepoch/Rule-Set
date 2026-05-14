# Clash Rules

个人维护的 mihomo (Clash Meta) 规则集合。

## 📁 仓库结构

```
clash-rules/
├── domain/                          # 我自己维护的纯域名规则
│   ├── cloud-drive.list            # 网盘下载（Google Drive/OneDrive/Dropbox 等）
│   ├── social-media.list           # 社交媒体（X/Reddit/Discord/Telegram 等）
│   └── ai-services.list            # AI 服务（Claude/ChatGPT/Gemini 等）
├── upstream/                        # 上游同步的规则集（GitHub Actions 自动同步）
│   └── HosheaPDNX/
│       ├── VERSION                 # 当前同步的上游版本
│       ├── mihomo/                 # Mihomo 格式规则（mrs/yaml）
│       └── sing-box/               # sing-box 格式规则
├── mrs/                             # 我的规则编译为 mrs（GitHub Actions 自动）
└── .github/workflows/
    ├── compile-mrs.yml             # 自动编译我的规则到 mrs
    └── sync-upstream.yml           # 自动同步上游规则
```

## 🚀 在 mihomo 配置中使用

### 我维护的规则

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

  ai-services:
    type: http
    behavior: domain
    format: text
    url: "https://raw.githubusercontent.com/Grepoch/clash-rules/main/domain/ai-services.list"
    path: ./ruleset/ai-services.list
    proxy: DIRECT
    interval: 86400

rules:
  - RULE-SET,cloud-drive,💾 网盘下载
  - RULE-SET,social-media,📱 社交媒体
  - RULE-SET,ai-services,🤖 AI服务
```

### 上游同步规则（HosheaPDNX）

```yaml
rule-providers:
  Google-Site:
    type: http
    behavior: domain
    format: mrs
    url: "https://raw.githubusercontent.com/Grepoch/clash-rules/main/upstream/HosheaPDNX/mihomo/Google/Google-Site.mrs"
    path: ./ruleset/Google-Site.mrs
    proxy: DIRECT
    interval: 86400
```

### 国内 CDN 加速

```
原始: https://raw.githubusercontent.com/Grepoch/clash-rules/main/...
加速: https://cdn.jsdmirror.com/gh/Grepoch/clash-rules@main/...
```

## 📋 规则集说明

详见 [domain/](./domain/) 和 [upstream/README.md](./upstream/README.md)。

## 🔄 自动更新机制

| 工作流 | 频率 | 作用 |
|--------|------|------|
| `compile-mrs.yml` | push 触发 | 把 `domain/*.list` 编译为 `mrs/*.mrs` |
| `sync-upstream.yml` | 每日 UTC 02:00 | 同步 HosheaPDNX/rule-set 最新 tag |

mihomo 客户端会按 `interval`（默认 86400 秒 = 24 小时）自动拉取最新规则。

## 🛠️ 维护

```bash
# 修改自己的规则
vim domain/cloud-drive.list

# 提交并推送
git add . && git commit -m "feat: add new domain" && git push
```

## 📜 License

- 本仓库 `domain/` 和 `mrs/` 内容遵循 [MIT License](./LICENSE)
- `upstream/` 目录遵循各自上游项目的许可证
