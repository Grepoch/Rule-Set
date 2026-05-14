# Upstream Rule Sets

此目录存放从上游仓库同步的规则集，由 GitHub Actions 自动维护。

## 同步源

### HosheaPDNX/rule-set

- **上游**: https://github.com/HosheaPDNX/rule-set
- **License**: 见 `HosheaPDNX/UPSTREAM_LICENSE`
- **同步频率**: 每日 UTC 02:00（北京时间 10:00）
- **当前版本**: 见 `HosheaPDNX/VERSION`
- **同步内容**:
  - `mihomo/` — Mihomo (Clash Meta) 格式规则
  - `sing-box/` — sing-box 格式规则

## 引用方式

### Mihomo (mrs)

```yaml
rule-providers:
  Apple-Site:
    type: http
    behavior: domain
    format: mrs
    url: "https://raw.githubusercontent.com/Grepoch/clash-rules/main/upstream/HosheaPDNX/mihomo/Apple/Apple-Site.mrs"
    path: ./ruleset/Apple-Site.mrs
    proxy: DIRECT
    interval: 86400
```

### 国内 CDN 加速

```yaml
url: "https://cdn.jsdmirror.com/gh/Grepoch/clash-rules@main/upstream/HosheaPDNX/mihomo/Apple/Apple-Site.mrs"
```

## 可用规则集（HosheaPDNX）

mihomo 目录下的分类（每个分类含 `-Site.mrs`、`-IP.mrs`、`-Site.yaml`、`-IP.yaml`、`-Site-Classical.yaml`、`-IP-Classical.yaml` 等格式）：

- 12306（中国铁路）
- AD（广告拦截）
- AI（AI 服务，含 OpenAI/Claude/Gemini 等）
- Apple
- Bahamut（巴哈姆特）
- Bilibili
- China（国内站点/IP）
- DNS
- Discord
- GFWList
- Games（游戏）
- Google
- GoogleFCM（Google 推送）
- Local（局域网）
- Messages（消息类）
- Microsoft
- Netflix
- OpenAI
- Pixiv
- Speedtest
- Spotify
- Steam
- SteamCN
- Telegram
- TikTok

## 维护

如需手动触发同步，进入仓库 Actions 页面 → Sync Upstream Rules → Run workflow。

## 法律声明

`upstream/` 目录下的内容是上游开源项目的复制品，遵循其原始许可证。修改请直接向上游提交 PR。
