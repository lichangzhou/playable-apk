# playable-apk

**Playable 的 OTA 分发仓库** —— 正式签名的 APK 托管与版本清单。

这个仓库不是 Playable 的源码仓库。源码与项目主页在
[lichangzhou/Playable](https://github.com/lichangzhou/Playable)。

## 下载

最新版本清单见 [`version.json`](version.json)，其中 `apk` 字段是直链。
历史版本见 [Releases](https://github.com/lichangzhou/playable-apk/releases)。

| 平台 | 说明 |
|---|---|
| Android 手机 / 平板 | 直接下载 APK 安装，首次安装需允许「未知来源」 |
| Android TV | 同上，TV 版为独立 APK |
| Windows / iOS | 走 [Playable 仓库](https://github.com/lichangzhou/Playable) 的构建说明 |

APK 使用正式证书签名（SHA-256 `fed595e7…`），**可覆盖安装，不丢数据**。

## 遇到问题？

按问题类型选入口，全部都在 GitHub 上：

| 想反馈什么 | 入口 |
|---|---|
| 装不上、下载失败、签名报错 | [提 issue](https://github.com/lichangzhou/playable-apk/issues/new) |
| 激活 / 许可证问题 | [提 issue](https://github.com/lichangzhou/playable-apk/issues/new)，请注明**设备型号 + Android 版本 + 完整报错文字** |
| 播放功能 BUG、崩溃 | [Playable 仓库提 issue](https://github.com/lichangzhou/Playable/issues/new?template=bug_report.yml) |
| 使用问题、怎么配置 | [Playable 讨论区](https://github.com/lichangzhou/Playable/discussions) |

⚠️ **不要在 issue 里贴激活码、设备指纹或服务器地址**，请先脱敏。

## 版本记录

Release notes 记录每个版本的完整改动。当前版本与更新日志：

```json
{
  "versionCode": 91,
  "versionName": "1.1.55"
}
```

## License

APK 分发与商业授权另行约定，详见 [Playable 仓库](https://github.com/lichangzhou/Playable#license)。
