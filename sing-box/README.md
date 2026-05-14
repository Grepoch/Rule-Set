# sing-box 规则集

sing-box 格式的规则集（JSON），由 `mihomo/` 目录下的 `.list` 文件转换生成。

## 目录

| 分类 | 文件 |
|------|------|
| CloudDrive | `CloudDrive/CloudDrive-Site.json` |
| SocialMedia | `SocialMedia/SocialMedia-Site.json` |
| AI | `AI/AI-Site.json` |

## 引用方式

```json
{
  "route": {
    "rule_set": [
      {
        "tag": "cloud-drive",
        "type": "remote",
        "format": "source",
        "url": "https://raw.githubusercontent.com/Grepoch/clash-rules/main/sing-box/CloudDrive/CloudDrive-Site.json"
      }
    ]
  }
}
```
