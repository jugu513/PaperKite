# Paperkite 纸鸢 · 本地优先的电子书阅读器

> 一个单文件 HTML 就能跑起来的阅读器，和一个 3MB 的 Windows 桌面壳。
> 不依赖账号、不上云、数据永远在自己手里。

Paperkite（纸鸢）支持 15 种电子书格式、本地优先存储、AI 能力可选接入、朗读可离线可用。它有两种形态，同一套前端：

- **HTML 版**（`paperkite.html`）：单文件，浏览器打开即用，可离线保存随身携带
- **Desktop 版**（`desktop/`）：Tauri 2 壳 + WebView2 内核，安装包约 3MB，数据落在 `文档/paperkite/`

## 为什么会有它

市面上的阅读器要么绑账号、要么绑云、要么重得离谱。Paperkite 的核心理念是**轻装上阵**：单文件便携、数据自主、要什么能力自己决定加什么。它最初只是作者自己的工具，功能都是从真实使用里写出来的。现在把它开源，希望也能帮到同样喜欢「数据在自己手里」的人。

## 功能

- **15 种格式**：TXT / EPUB / MOBI / AZW3 / AZW / PDF / DOCX / FB2 / HTML / XML / XHTML / MHTML / DJVU / MD / 纯文本
- **本地优先**：书架、笔记、高亮、进度全部存本地（localStorage / IndexedDB / OPFS），不经过任何服务器
- **WebDAV 同步**：可选开关，自备 WebDAV（坚果云等）即可跨设备同步
- **AI 能力（可选）**：对话 / 问书 / 摘要 / 角色档案 / 情感曲线 / 小测 / 跨书推荐 / 段落解析 / 智能分章 / 思维导图 / AI 词典——全部自备 API key，仅存本地
- **朗读（TTS）**：Edge 在线 / 小米 MiMo / 浏览器离线三引擎自动切换；句子切分、角色朗读、音频缓存、插件引擎
- **扫描版 PDF OCR**：文本层为空时按需加载 Tesseract.js（平时零依赖）
- **更多**：OPDS 订阅、加密导出、番茄钟、环境声、命令面板、PIN 锁、插件脚本……

## 快速开始

### HTML 版（零安装）

1. 下载 `paperkite.html`（单文件）
2. 浏览器打开即可（推荐 Chrome / Edge）

### Desktop 版（Windows）

1. 从 [Releases](../../releases) 下载安装包（约 3MB）
2. 安装后数据自动落在 `文档/paperkite/`
3. 关闭窗口 = 隐藏到托盘（朗读不中断）

> 安装包未做代码签名，首次运行 Windows SmartScreen 可能提示「未知发布者」——点「仍要运行」即可，属正常现象。

### 从源码构建 Desktop（需 Windows + Rust）

```bash

rustup default stable

cd desktop

cargo tauri build

# 产物: src-tauri/target/release/bundle/nsis/*_x64-setup.exe

```

## 数据与隐私

- **数据全部在本地**：书架/笔记/高亮/设置存在本地存储，用户可见、可备份
- **AI 密钥仅存本地**：你填的 API key 只保存在本地，不上传任何服务器
- **内置 TTS 兜底密钥**：为开箱即用，内置买免费 MiMo TTS
- **WebDAV 同步**：仅在开启后，按你配置的地址和间隔上传/拉取

## 安全边界

- **插件 = 你信任的代码**：TTS 插件和脚本目录里的 JS 会在本地执行，请只加载你信任的脚本（与浏览器扩展的信任模型一致）
- **OCR 依赖 CDN**：扫描版 PDF 首次使用才联网加载依赖，平时零网络依赖

## 目录结构

```

paperkite/

├── paperkite.html      # HTML 版（单文件）

├── desktop/            # Desktop 版（Tauri 壳）

│   ├── frontend/       #   前端副本（CI 强制与根目录一致）

│   └── src-tauri/      #   Rust 壳源码

└── .github/workflows/  # CI（Pages 部署 / Windows 构建）

```
