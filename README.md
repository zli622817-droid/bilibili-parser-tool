# B站解析工具（普通版 / 登录版 / Cookie 提取）

一个 Windows 桌面工具，用于解析并下载 B 站视频，支持音视频分离下载后自动合并为 MP4。
本仓库提供**源码、Cookie 提取工具**与**可直接使用的安装包/自解压程序**。

> ⚠️ 仅供个人学习与交流使用，请尊重原作者与平台版权，下载内容请在 24 小时内删除，请勿用于任何商业用途或二次分发他人作品。

---

## ✨ 功能

- 输入 **链接 或 BV 号** 一键解析
- 自动获取**标题**与**全部可用清晰度**（优先级排序）
- 清晰度下拉选择，支持 **1080P / 720P / 480P / 360P** 等
- 音视频**分开下载**，完成后调用 `ffmpeg` **自动合并为 MP4**，并清理临时文件
- 实时进度条、下载速度、已下载/总大小、运行日志
- 异常捕获（链接错误 / 网络失败 / 解析失败均弹窗提示）
- 自定义保存路径，**默认自动检测桌面**，并**记忆上次保存位置与窗口位置/大小**
- **登录版**可粘贴 Cookie，解锁 **1080P 高码率 / 60 帧 / 4K** 等大会员画质
- **Cookie 有效性检测**（校验是否登录、是否为大会员）
- 圆角卡片 UI、自适应 DPI 缩放、无边框

---

## 📦 版本说明

| 版本 | 说明 |
| --- | --- |
| **普通版** | 免登录，下载公开可下的清晰度 |
| **登录版** | 可填 Cookie，解锁 1080P高码率 / 60帧 / 4K |
| **Cookie 提取工具** | 一键抓取浏览器登录 Cookie（Playwright 驱动本机 Edge） |
| **登录版自解压** | 双击静默解压到 exe 同目录，无需安装 |
| **安装包（Inno / NSIS）** | 标准安装器，装到 Program Files，含卸载 |

> 体积较大的安装包/自解压程序请从 **右侧 Releases** 下载，不要直接放进 Git 仓库（详见「下载」）。

---

## 🚀 快速开始（源码运行）

需要 Python 3.9+：

```bash
pip install yt-dlp
```

下载 `ffmpeg.exe` 并放到脚本同目录（[ffmpeg 下载](https://ffmpeg.org/download.html)），然后：

```bash
python bilibili_gui.py        # 普通版
python bilibili_gui_login.py  # 登录版（可填 Cookie）
python cookie_extractor.py    # Cookie 提取工具
```

依赖：`pip install yt-dlp`（登录版另含 Cookie 检测，无需额外依赖；Cookie 提取工具需 `pip install playwright`，复用系统 Edge，无需下载浏览器）。

---

## 🎯 登录版：如何解锁 4K

1. 浏览器登录 B 站（需为**大会员**账号，否则最高 1080P）。
2. 用「Cookie 提取工具」打开 bilibili 并扫码登录，点【提取并复制 Cookie】；会**自动复制并保存**到配置。
3. 打开「登录版」，它会**自动读取**已保存的 Cookie；或手动粘贴、点【粘贴】。
4. 点【检测 Cookie 有效性】确认状态（显示 是否登录 / 是否为大会员）。
5. 解析视频，即可看到 1080P 高码率 / 60 帧 / 4K 等画质。

> Cookie 会随退出登录/清缓存失效，失效后重新提取一遍即可。程序不会上传你的 Cookie，Cookie 仅保存在本机 `%APPDATA%\.bili_downloader_config.json`，**不会打入任何安装包**。

---

## 🧩 目录结构

```
├─ bilibili_gui.py            # 普通版源码
├─ bilibili_gui_login.py      # 登录版源码（含 Cookie 检测）
├─ cookie_extractor.py        # Cookie 提取工具源码（Playwright）
├─ sfx_extract.py             # 自解压器生成脚本
├─ B站解析工具安装包.iss       # Inno Setup 安装脚本
└─ README.md
```

---

## 🛠 打包（自行构建）

安装包由 **Inno Setup 6** 制作（`Compil32`/`ISCC.exe`），Modern 主题 + 中文语言：

```text
ISCC.exe "B站解析工具安装包.iss"
```

安装包打包的源目录为 `融合\`（普通版 exe + 登录版 exe 共享同一份 `_internal`/ffmpeg，减小体积）。

---

## ⬇️ 下载

- 可直接运行的安装包 / 自解压程序体积较大（约 90MB），请从 **GitHub Releases 页面**下载对应 `.exe`。
- 源码与脚本请用 `git clone` 或 Download ZIP 获取。

> GitHub 普通仓库单文件大小上限为 100MB，因此**不要**把 ≥100MB 的 exe 提交到仓库，请上传到 **Releases 的附件**。

---

## 📄 许可

本项目基于 **MIT License** 发布，详见 [LICENSE](LICENSE)。

仅供学习使用，请遵守 B 站用户协议与相关法律法规。作者不对使用本工具造成的任何后果负责。
