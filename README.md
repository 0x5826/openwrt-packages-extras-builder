# OpenWrt Packages Extras 自动构建仓库

本仓库通过 GitHub Actions 基于官方 OpenWrt SDK 自动编译 [0x5826/openwrt-packages-extras](https://github.com/0x5826/openwrt-packages-extras) 中的全部软件包，并按 OpenWrt 大版本、包格式与目标架构发布至 GitHub Releases。

## 发布结构

按大版本拆分为三个滚动 Release，各自保留最新构建的单包文件、全量压缩包与 `SHA256SUMS.txt`：

| Release 标签 | OpenWrt 版本 | 源码分支 | 包格式 | 目标架构 | 产物说明 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `latest-25.12` | 25.12.6 | `main` | `.apk` / `.ipk` | `x86_64` / `aarch64_generic` / `aarch64_cortex-a53` / `noarch` | 单个 `.apk`（架构包后缀区分）与 `.ipk` 直传 + 分架构 `.tar.gz` 总包 |
| `latest-24.10` | 24.10.8 | `main` | `.ipk` | `x86_64` / `aarch64_generic` / `aarch64_cortex-a53` / `noarch` | 原生单个 `.ipk` 直传 + 分架构 `.tar.gz` 总包 |
| `latest-21.02` | 21.02.7 | `openwrt-21.02` | `.ipk` | `x86_64` / `aarch64_generic` / `aarch64_cortex-a53` / `noarch` | 原生单个 `.ipk` 直传 + 分架构 `.tar.gz` 总包 |

## 触发与更新规则

- **定时增量检测**：每日 UTC 02:00 检查上游 `main` 与 `openwrt-21.02` 最新提交，任一发布标签与上游不一致时自动触发构建。
- **手动触发**：在 GitHub Actions 页面执行 `Build OpenWrt Packages (.apk & .ipk)`，可按需覆盖各系列 OpenWrt 版本号。
- **滚动覆盖**：每次构建完成后自动覆盖对应大版本的 `latest-*` Release。
