# Rule-Set

精细化代理分流规则集，支持 Mihomo (Clash Meta)。

## 目录结构

```
Rule-Set/
├── mihomo/                  # Classical 格式（含规则类型前缀）
│   ├── AI.txt              # AI 服务合集
│   ├── Claude.txt          # Claude / Anthropic
│   ├── OpenAI.txt          # ChatGPT / OpenAI
│   ├── Gemini.txt          # Gemini / Google AI
│   ├── Copilot.txt         # GitHub Copilot / Microsoft Copilot
│   ├── CloudDrive.txt      # Google Drive 全域名
│   ├── OneDrive.txt        # OneDrive / SharePoint
│   ├── Download.txt        # 网盘下载合集
│   ├── Twitter.txt         # X (Twitter)
│   ├── Facebook.txt        # Facebook / Messenger
│   ├── Instagram.txt       # Instagram / Threads
│   ├── Telegram.txt        # Telegram
│   ├── Discord.txt         # Discord
│   ├── Reddit.txt          # Reddit
│   ├── SocialMedia.txt     # 社交媒体合集
│   ├── YouTube.txt         # YouTube
│   ├── Netflix.txt         # Netflix
│   ├── Spotify.txt         # Spotify
│   ├── Google.txt          # Google 服务
│   ├── Microsoft.txt       # Microsoft 服务
│   ├── Apple.txt           # Apple 服务
│   ├── GitHub.txt          # GitHub
│   ├── Steam.txt           # Steam
│   ├── TikTok.txt          # TikTok
│   └── Speedtest.txt       # 测速
│
├── mihomo/domain/           # Domain 格式（纯域名，可编译为 mrs）
│   ├── AI.txt / AI.mrs
│   ├── Claude.txt / Claude.mrs
│   ├── ...
│   └── (同上，每个分类对应 .txt + .mrs)
│
└── mihomo/ip/               # IP 格式（预留）
```

## 使用方法

### Classical 格式（behavior: classical）

适用于混合规则类型（DOMAIN + DOMAIN-SUFFIX + DOMAIN-KEYWORD）：

```yaml
rule-providers:
  AI:
    type: http
    behavior: classical
    format: text
    url: "https://raw.githubusercontent.com/Grepoch/Rule-Set/main/mihomo/AI.txt"
    path: ./ruleset/AI.txt
    proxy: DIRECT
    interval: 86400

rules:
  - RULE-SET,AI,🤖 AI服务
```

### Domain 格式（behavior: domain，推荐）

性能更好，支持编译为 mrs 二进制：

```yaml
rule-providers:
  AI:
    type: http
    behavior: domain
    format: mrs
    url: "https://raw.githubusercontent.com/Grepoch/Rule-Set/main/mihomo/domain/AI.mrs"
    path: ./ruleset/AI.mrs
    proxy: DIRECT
    interval: 86400
```

### CDN 加速

```
https://cdn.jsdmirror.com/gh/Grepoch/Rule-Set@main/mihomo/domain/AI.mrs
```

## 规则集说明

### AI 服务

| 文件 | 覆盖 |
|------|------|
| `AI.txt` | 全部 AI 平台合集 |
| `Claude.txt` | Anthropic / Claude |
| `OpenAI.txt` | ChatGPT / Sora / OpenAI API |
| `Gemini.txt` | Gemini / AI Studio / DeepMind |
| `Copilot.txt` | GitHub Copilot / Microsoft Copilot |

### 网盘下载

| 文件 | 覆盖 |
|------|------|
| `Download.txt` | 全部网盘合集 |
| `CloudDrive.txt` | Google Drive / Docs / Sheets / Photos（含 googleapis 子域） |
| `OneDrive.txt` | OneDrive / SharePoint |

### 社交媒体

| 文件 | 覆盖 |
|------|------|
| `SocialMedia.txt` | 全部社交平台合集 |
| `Twitter.txt` | X (Twitter) |
| `Facebook.txt` | Facebook / Messenger |
| `Instagram.txt` | Instagram / Threads |
| `Telegram.txt` | Telegram |
| `Discord.txt` | Discord |
| `Reddit.txt` | Reddit |

### 流媒体

| 文件 | 覆盖 |
|------|------|
| `YouTube.txt` | YouTube |
| `Netflix.txt` | Netflix |
| `Spotify.txt` | Spotify |

### 服务

| 文件 | 覆盖 |
|------|------|
| `Google.txt` | Google 全服务 |
| `Microsoft.txt` | Microsoft / Office 365 |
| `Apple.txt` | Apple |
| `GitHub.txt` | GitHub |
| `Steam.txt` | Steam |
| `TikTok.txt` | TikTok |
| `Speedtest.txt` | Speedtest / Fast.com |

## 自动化

| 工作流 | 触发 | 作用 |
|--------|------|------|
| `compile-mrs.yml` | push `mihomo/domain/*.txt` | 编译 .txt → .mrs |
| `check-upstream.yml` | 每周一 / 手动 | 检查 HosheaPDNX/rule-set 更新 |

## 参考

- [HosheaPDNX/rule-set](https://github.com/HosheaPDNX/rule-set)
- [666OS/rules](https://github.com/666OS/rules)
- [MetaCubeX/meta-rules-dat](https://github.com/MetaCubeX/meta-rules-dat)

## License

MIT
