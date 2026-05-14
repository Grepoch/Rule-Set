# Clash Rules

个人维护的 mihomo (Clash Meta) 规则集合，专注于精细化分流。

## 📁 仓库结构

```
clash-rules/
├── domain/                          # 规则文件（手动维护）
│   ├── cloud-drive.list            # 网盘下载（Google Drive/OneDrive/Dropbox 等）
│   ├── social-media.list           # 社交媒体（X/Reddit/Discord/Telegram 等）
│   └── ai-services.list            # AI 服务（Claude/ChatGPT/Gemini 等）
├── mrs/                             # 自动编译的 mrs 二进制格式
│   ├── cloud-drive.mrs
│   ├── social-media.mrs
│   └── ai-services.mrs
├── .upstream-version                # 上游版本跟踪（HosheaPDNX/rule-set）
└── .github/workflows/
    ├── compile-mrs.yml             # push 时自动编译 .list → .mrs
    └── check-upstream.yml          # 每周检查上游更新 → 创建 Issue 通知
```

## 🚀 在 mihomo 配置中使用

### text 格式（推荐，易调试）

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
```

### mrs 格式（性能更好）

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

### 国内 CDN 加速

```
原始: https://raw.githubusercontent.com/Grepoch/clash-rules/main/...
加速: https://cdn.jsdmirror.com/gh/Grepoch/clash-rules@main/...
```

## 🔄 上游跟踪

本仓库参考 [HosheaPDNX/rule-set](https://github.com/HosheaPDNX/rule-set) 的规则，但**不自动同步**。

- GitHub Actions 每周一检查上游是否有新版本
- 如有更新，自动创建 Issue 通知，包含变更对比链接
- 由我人工审核后决定是否采纳到 `domain/` 目录

当前跟踪版本：见 `.upstream-version`

## 🛠️ 维护

```bash
# 编辑规则
vim domain/cloud-drive.list

# 提交并推送（自动触发 mrs 编译）
git add . && git commit -m "feat: add new domain" && git push
```

## 📜 License

MIT
