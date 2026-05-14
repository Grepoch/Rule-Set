# Clash Rules

个人维护的代理规则集合，支持多内核格式。

## 📁 仓库结构

```
clash-rules/
├── mihomo/                          # Mihomo (Clash Meta) 格式
│   ├── AI/
│   │   ├── AI-Site.list            # text 格式（源文件）
│   │   ├── AI-Site.mrs             # mrs 二进制（自动编译）
│   │   └── README.md
│   ├── CloudDrive/
│   │   ├── CloudDrive-Site.list
│   │   ├── CloudDrive-Site.mrs
│   │   └── README.md
│   └── SocialMedia/
│       ├── SocialMedia-Site.list
│       ├── SocialMedia-Site.mrs
│       └── README.md
├── sing-box/                        # sing-box 格式
│   ├── AI/
│   │   └── AI-Site.json
│   ├── CloudDrive/
│   │   └── CloudDrive-Site.json
│   └── SocialMedia/
│       └── SocialMedia-Site.json
├── .upstream-version                # 上游版本跟踪
└── .github/workflows/
    ├── compile-mrs.yml             # 自动编译 .list → .mrs
    └── check-upstream.yml          # 每周检查上游更新
```

## 🚀 引用方式

### Mihomo — text 格式

```yaml
rule-providers:
  CloudDrive-Site:
    type: http
    behavior: domain
    format: text
    url: "https://raw.githubusercontent.com/Grepoch/clash-rules/main/mihomo/CloudDrive/CloudDrive-Site.list"
    path: ./ruleset/CloudDrive-Site.list
    proxy: DIRECT
    interval: 86400
```

### Mihomo — mrs 格式（推荐，性能更好）

```yaml
rule-providers:
  CloudDrive-Site:
    type: http
    behavior: domain
    format: mrs
    url: "https://raw.githubusercontent.com/Grepoch/clash-rules/main/mihomo/CloudDrive/CloudDrive-Site.mrs"
    path: ./ruleset/CloudDrive-Site.mrs
    proxy: DIRECT
    interval: 86400
```

### sing-box

```json
{
  "tag": "cloud-drive",
  "type": "remote",
  "format": "source",
  "url": "https://raw.githubusercontent.com/Grepoch/clash-rules/main/sing-box/CloudDrive/CloudDrive-Site.json"
}
```

### 国内 CDN 加速

```
原始: https://raw.githubusercontent.com/Grepoch/clash-rules/main/...
加速: https://cdn.jsdmirror.com/gh/Grepoch/clash-rules@main/...
```

## 📋 规则集列表

| 分类 | 说明 | 覆盖平台 |
|------|------|----------|
| **AI** | AI 服务 | Claude、ChatGPT、Gemini、Copilot、Perplexity、Midjourney 等 |
| **CloudDrive** | 网盘下载 | Google Drive、OneDrive、Dropbox、MEGA、iCloud、Box 等 |
| **SocialMedia** | 社交媒体 | X、Reddit、Discord、Telegram、Facebook、WhatsApp、Signal 等 |

## 🔄 自动化

| 工作流 | 触发条件 | 作用 |
|--------|----------|------|
| `compile-mrs.yml` | push `mihomo/**/*.list` | 编译 .list → .mrs |
| `check-upstream.yml` | 每周一 / 手动 | 检查 HosheaPDNX/rule-set 更新 → 创建 Issue |

## 🔗 上游参考

- [HosheaPDNX/rule-set](https://github.com/HosheaPDNX/rule-set) — 当前跟踪版本见 `.upstream-version`
- [MetaCubeX/meta-rules-dat](https://github.com/MetaCubeX/meta-rules-dat) — mihomo 官方规则数据

## 🛠️ 维护

```bash
# 编辑规则（修改 .list 源文件）
vim mihomo/CloudDrive/CloudDrive-Site.list

# 提交推送（自动触发 mrs 编译）
git add . && git commit -m "feat: add new domain" && git push
```

## 📜 License

MIT
