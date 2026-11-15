# OpenWrt Packages Extras 自动构建仓库

本仓库通过 GitHub Actions 基于官方 OpenWrt SDK 自动编译 [0x5826/openwrt-packages-extras](https://github.com/0x5826/openwrt-packages-extras) 中的全部软件包，并按分支、包格式与目标架构打包发布至 GitHub Releases（固定保留最新 `latest` 发布）。

## 构建矩阵

| OpenWrt 版本 | 源码分支 | 包格式 | 目标架构 | 产物说明 |
| :--- | :--- | :--- | :--- | :--- |
| 25.12.6 | `main` | `.apk` / `.ipk` | `x86_64` / `aarch64_generic` / `aarch64_cortex-a53` / `noarch` | 同时提供 `.apk` 与 `.ipk` 两套归档包 |
| 24.10.8 | `main` | `.ipk` | `x86_64` / `aarch64_generic` / `aarch64_cortex-a53` / `noarch` | 含架构二进制包与 `luci-app-*` 通用包 |
| 21.02.7 | `openwrt-21.02` | `.ipk` | `x86_64` / `aarch64_generic` / `aarch64_cortex-a53` / `noarch` | 含架构二进制包与 `luci-app-*` 通用包 |

## 触发与发布规则

- **定时构建**：每日 UTC 02:00 检查上游 `main` 与 `openwrt-21.02` 最新提交，存在变更时自动触发构建。
- **手动触发**：在 GitHub Actions 页面执行 `Build OpenWrt Packages (.apk & .ipk)`，可按需覆盖 OpenWrt 版本号。
- **滚动发布**：每次构建完成后自动覆盖更新 `latest` Release，页面仅保留最新全量产物与 `SHA256SUMS.txt`。
