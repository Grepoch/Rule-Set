# SocialMedia 社交媒体

覆盖以下平台：

- **微博客/社区** — X (Twitter)、Reddit、Threads、Tumblr、Mastodon、Bluesky
- **Meta 系** — Facebook、Instagram
- **即时通讯** — Telegram、Discord、WhatsApp、Signal、LINE、Viber、Skype
- **直播** — Twitch
- **职场** — LinkedIn、Slack
- **其他** — Pinterest、Snapchat、Clubhouse

## 文件

| 文件 | 格式 | 用途 |
|------|------|------|
| `SocialMedia-Site.list` | text | mihomo rule-provider (behavior: domain) |
| `SocialMedia-Site.mrs` | mrs | mihomo rule-provider (behavior: domain, 高性能) |

## 引用

```yaml
rule-providers:
  SocialMedia-Site:
    type: http
    behavior: domain
    format: mrs
    url: "https://raw.githubusercontent.com/Grepoch/clash-rules/main/mihomo/SocialMedia/SocialMedia-Site.mrs"
    path: ./ruleset/SocialMedia-Site.mrs
    proxy: DIRECT
    interval: 86400
```
