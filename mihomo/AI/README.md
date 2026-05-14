# AI 人工智能服务

覆盖以下平台：

- **Anthropic** — Claude
- **OpenAI** — ChatGPT、Sora、API
- **Google AI** — Gemini、AI Studio、DeepMind
- **GitHub Copilot** / **Microsoft Copilot**
- **其他** — Perplexity、Poe、Midjourney、Civitai、HuggingFace、Replicate、Stability AI、Runway、Suno、ElevenLabs、Character.ai、Kimi、You.com

## 文件

| 文件 | 格式 | 用途 |
|------|------|------|
| `AI-Site.list` | text | mihomo rule-provider (behavior: domain) |
| `AI-Site.mrs` | mrs | mihomo rule-provider (behavior: domain, 高性能) |

## 引用

```yaml
rule-providers:
  AI-Site:
    type: http
    behavior: domain
    format: mrs
    url: "https://raw.githubusercontent.com/Grepoch/clash-rules/main/mihomo/AI/AI-Site.mrs"
    path: ./ruleset/AI-Site.mrs
    proxy: DIRECT
    interval: 86400
```
