# playable-apk

**Playable 的 OTA 分发仓库** —— 正式签名的 APK 托管与版本清单。

这个仓库不是 Playable 的源码仓库。源码与项目主页在
[lichangzhou/Playable](https://github.com/lichangzhou/Playable)。

## 当前版本

**v77 · 1.1.66 · versionCode 102**（2026-11-23 发布）

最新版本清单见 [`version.json`](version.json)，其中 `apk` 字段是直链。
历史版本见 [Releases](https://github.com/lichangzhou/playable-apk/releases)。
三源同步分发：GitHub + Gitee + jsDelivr（CDN），任一源都能拿到最新版本。

## 下载

| 平台 | 说明 |
|---|---|
| Android 手机 / 平板 | 直接下载 APK 安装，首次安装需允许「未知来源」 |
| Android TV | 同上，TV 版为独立 APK |
| Windows / iOS | 走 [Playable 仓库](https://github.com/lichangzhou/Playable) 的构建说明 |

APK 使用正式证书签名（SHA-256 `fed595e7…`），**可覆盖安装，不丢数据**。
OTA 升级无需卸载，服务器配置、歌词缓存、播放队列等本地数据全部保留。

## 功能总览

Playable 是面向 Android（手机 / 平板 / TV）的一体化媒体播放器，采用**自研播放内核**，
覆盖视频、直播、音乐与付费功能。以下是截至 v77 已落地的全部功能与进展。

### 🎬 视频播放（自研内核）
- **自研原生内核**（libplaynative.so，覆盖 arm64 / armv7a / x86 / x86_64 四 ABI），已彻底移除 Media3 / ExoPlayer 依赖。
- **进度条体验**：点选进度条钉位不回跳、拖动停在目标位置、seek 后音画字幕同步，修复拖动导致的永久偏移。
- **音画同步**：seek 后延迟视频起锚、等音频实播就绪再出帧，消除音频 FIFO 填充期被固化的偏移。
- **起播音频**：go-gate 门控（音频等视频 primed 再出声）消除起始约 0.3s 偏差；pre-roll 缓冲消除起播 underrun 卡顿。
- **字幕**：ASS / PGS 位图字幕渲染、双语同显（第二条字幕）、字幕颜色设置（含自动）、字幕选择状态修复；Emby SRT API 自动拉取。
- **媒体源**：HTTP(S)（含 302 重定向直连）、WebDAV、SMB（jcifs-ng）、本地文件；支持 **ISO 原盘**播放。
- **换链自愈**（StrmUrlRecovery）：播放失效时自动换链并恢复，无需手动重进。
- **画中画（PiP）**：全屏播放与 PiP 切换，修复回到桌面后 PiP 异常。

### 📺 直播（Live）
- **M3U 源管理**：增删源（DataStore 持久化），频道列表含台标 / 频道号 / 分组 / 收藏置顶。
- **EPG 电子节目单**（XMLTV）。
- **Xtream Codes** 源支持。
- **频道管理**：排序 / 隐藏 / 分组。
- **播放体验**：直播音画同步修复、关闭播放器退出 APP、失效频道兜底、时移回看。
- 收藏 / 隐藏大按钮化，贴合 TV 遥控操作。

### 🎵 音乐（Music）
- **音乐源发现**：Emby / Jellyfin 音乐库（分页拉取，支持数万首大库）、本机文件夹（SAF）、自动扫描开关。
- **曲库解析**：从目录结构解析歌手 / 专辑（路径解析，向上回溯兼容 CD1/CD2），不再依赖服务器标签；歌手头像自动联网补全。
- **歌词**：QQ 音乐（主力）+ 网易云（兜底）+ LRCLIB 多源，全屏歌词页。
- **队列**：Musicolet 式多队列（多条独立队列 / 位置冻结 / 无损编辑 / 撤销），队列快照 + 重扫自愈。
- **页面**：全屏歌词页、歌手列表 / 详情页、专辑网格。
- **DSP 音质**：RBJ EQ 双二阶（peaking / low-shelf / high-shelf）+ 全声道联动峰值 limiter，注入内核音频管线，按输出设备预设。

### 🔐 付费系统（专业版）
- **单一档位**：专业版 ¥68，由授权验证服务提供激活码校验。
- **设备上限**：每份许可最多 10 台激活设备。
- **功能闸门**：8 项付费功能，交互入口与内核使用点双重拦截，防止绕过。
- **云同步（CLOUD_SYNC）**：设置与播放进度推送到云端，新设备 / 重装后自动合并。
- **多客户端同步（MULTI_CLIENT_SYNC）**：媒体服务器列表推送到云端，在其他设备上自动合并。
- 云端用户数据存于授权验证服务容器内的 SQLite `sync_store` 表（按激活码存 JSON 快照），随服务持久化。
- 激活码输入做全角 / 半角归一化，避免输入法差异导致激活失败。

### 📡 TV 遥控
- 全主界面焦点基建（TvFocus）覆盖，底栏页签可遥控切换。
- 方向键 / OK / 返回 / 媒体键全通道：seek、播放暂停、控制条开关、页签切换。
- TV 专属首页 / 媒体库视图。

### 💬 弹幕
- 弹弹 Play 官方 API 对接，按当前视频自动搜索拉取，秒级时间轴，顶部 / 底部轨道分配。

### 📤 投屏
- DLNA / 投屏模块（CastProxy / DlnaCastController / CastSheet），支持投送到大屏并遥控。

## 版本进展

| 版本 | versionCode | versionName | 要点 |
|---|---|---|---|
| v77 | 102 | 1.1.66 | 云同步权益落地（云同步开关 + SyncManager 接线 + 服务端推送修复） |
| v76 | 101 | 1.1.65 | 进度条 seek 钉位 / 音画同步修复，横屏分栏布局 |
| v48 | 92 | 1.1.56 | 授权功能闸门双重拦截（8 项付费功能） |
| v32 | 71 | 1.1.35 | Music DSP（EQ / limiter 内核音频管线注入） |
| v31 | 70 | 1.1.34 | TV 遥控适配 |
| v30 | 69 | 1.1.33 | 收费系统三重修复 |

完整改动历史见各版本 [Release notes](https://github.com/lichangzhou/playable-apk/releases)。

## 遇到问题？

按问题类型选入口，全部都在 GitHub 上：

| 想反馈什么 | 入口 |
|---|---|
| 装不上、下载失败、签名报错 | [提 issue](https://github.com/lichangzhou/playable-apk/issues/new) |
| 激活 / 许可证问题 | [提 issue](https://github.com/lichangzhou/playable-apk/issues/new)，请注明**设备型号 + Android 版本 + 完整报错文字** |
| 播放功能 BUG、崩溃 | [Playable 仓库提 issue](https://github.com/lichangzhou/Playable/issues/new?template=bug_report.yml) |
| 使用问题、怎么配置 | [Playable 讨论区](https://github.com/lichangzhou/Playable/discussions) |

如果 issue / 讨论区不好用，也可以直接找我：

| 渠道 | 联系方式 |
|---|---|
| 邮箱 | `1543079796@qq.com` |
| QQ | `1543079796` |

⚠️ **不要在 issue 里贴激活码、设备指纹或服务器地址**，请先脱敏。

## License

APK 分发与商业授权另行约定，详见 [Playable 仓库](https://github.com/lichangzhou/Playable#license)。
