# Rule-Set

精细化代理分流规则集，支持 Mihomo (Clash Meta) 和 sing-box 内核。

专注于 AI 服务、网盘下载、社交媒体等场景的独立分流控制，适配住宅 IP / 数据中心 IP 等不同出口策略。

## 特性

- 按内核类型分目录，结构清晰
- 提供 `.list`（text）、`.mrs`（二进制）、`.json`（sing-box）三种格式
- GitHub Actions 自动编译 `.list` → `.mrs`
- 每周检查上游 [HosheaPDNX/rule-set](https://github.com/HosheaPDNX/rule-set) 更新并通知
- 规则手动审核维护，不盲目同步

## 目录结构

```
Rule-Set/
├── mihomo/                          # Mihomo (Clash Meta) 格式
│   ├── AI/                         # AI 服务
│   │   ├── AI-Site.list            # text 源文件
│   │   └── AI-Site.mrs             # 二进制（自动编译）
│   ├── CloudDrive/                 # 网盘下载
│   │   ├── CloudDrive-Site.list
│   │   └── CloudDrive-Site.mrs
│   └── SocialMedia/                # 社交媒体
│       ├── SocialMedia-Site.list
│       └── SocialMedia-Site.mrs
├── sing-box/                        # sing-box 格式
│   ├── AI/AI-Site.json
│   ├── CloudDrive/CloudDrive-Site.json
│   └── SocialMedia/SocialMedia-Site.json
└── .github/workflows/
    ├── compile-mrs.yml             # 自动编译
    └── check-upstream.yml          # 上游更新检查
```

## 规则集

| 分类 | 说明 | 覆盖平台 |
|------|------|----------|
| **AI** | AI 服务 | Claude、ChatGPT、Gemini、Copilot、Perplexity、Midjourney、HuggingFace 等 |
| **CloudDrive** | 网盘下载 | Google Drive、OneDrive、SharePoint、Dropbox、MEGA、iCloud、Box、WeTransfer 等 |
| **SocialMedia** | 社交媒体 | X、Reddit、Discord、Telegram、Facebook、Instagram、WhatsApp、Signal、LINE、Twitch、LinkedIn 等 |

## 使用方法

### Mihomo — mrs 格式（推荐）

```yaml
rule-providers:
  AI-Site:
    type: http
    behavior: domain
    format: mrs
    url: "https://raw.githubusercontent.com/Grepoch/Rule-Set/main/mihomo/AI/AI-Site.mrs"
    path: ./ruleset/AI-Site.mrs
    proxy: DIRECT
    interval: 86400

  CloudDrive-Site:
    type: http
    behavior: domain
    format: mrs
    url: "https://raw.githubusercontent.com/Grepoch/Rule-Set/main/mihomo/CloudDrive/CloudDrive-Site.mrs"
    path: ./ruleset/CloudDrive-Site.mrs
    proxy: DIRECT
    interval: 86400

  SocialMedia-Site:
    type: http
    behavior: domain
    format: mrs
    url: "https://raw.githubusercontent.com/Grepoch/Rule-Set/main/mihomo/SocialMedia/SocialMedia-Site.mrs"
    path: ./ruleset/SocialMedia-Site.mrs
    proxy: DIRECT
    interval: 86400

rules:
  - RULE-SET,AI-Site,🤖 AI服务
  - RULE-SET,CloudDrive-Site,💾 网盘下载
  - RULE-SET,SocialMedia-Site,📱 社交媒体
```

### Mihomo — text 格式

将 URL 中的 `.mrs` 替换为 `.list`，`format` 改为 `text`。

### sing-box

```json
{
  "route": {
    "rule_set": [
      {
        "tag": "ai-services",
        "type": "remote",
        "format": "source",
        "url": "https://raw.githubusercontent.com/Grepoch/Rule-Set/main/sing-box/AI/AI-Site.json"
      }
    ],
    "rules": [
      { "rule_set": "ai-services", "outbound": "ai-proxy" }
    ]
  }
}
```

### CDN 加速（国内访问）

```
https://cdn.jsdmirror.com/gh/Grepoch/Rule-Set@main/mihomo/AI/AI-Site.mrs
```

## 自动化

| 工作流 | 触发 | 作用 |
|--------|------|------|
| compile-mrs | push `mihomo/**/*.list` | 编译 text → mrs |
| check-upstream | 每周一 / 手动 | 检查 HosheaPDNX/rule-set 新版本 → 创建 Issue |

## 上游参考

- [HosheaPDNX/rule-set](https://github.com/HosheaPDNX/rule-set) — 规则参考来源
- [MetaCubeX/meta-rules-dat](https://github.com/MetaCubeX/meta-rules-dat) — mihomo 官方规则数据

## License

MIT
