# CloudDrive 网盘下载

覆盖以下平台：

- **Google Drive / Docs / Sheets / Slides** — 包括 `drivefrontend-pa.googleapis.com`、`signaler-pa.googleapis.com` 等关键 API
- **Google Photos** — `photos.google.com`
- **OneDrive / SharePoint** — `1drv.com`、`sharepoint.com`
- **iCloud Drive** — `icloud.com`、`icloud-content.com`
- **Dropbox** / **MEGA** / **Box** / **MediaFire** / **WeTransfer** / **pCloud** / **Sync**

## 文件

| 文件 | 格式 | 用途 |
|------|------|------|
| `CloudDrive-Site.list` | text | mihomo rule-provider (behavior: domain) |
| `CloudDrive-Site.mrs` | mrs | mihomo rule-provider (behavior: domain, 高性能) |

## 引用

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
