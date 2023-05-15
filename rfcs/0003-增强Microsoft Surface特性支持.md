# 增强 Microsoft Surface 特性支持

- 提案发起时间：2023-05-15
- 提案拉取请求：https://github.com/deepin-community/rfcs/pull/3

## 概要

本提案来自 [deepin-surface SIG](https://www.deepin.org/index/docs/sig/sig/deepin-surface/README.md)，旨在为 deepin 引入 [linux-surface](https://github.com/linux-surface) 组织中关于 Microsoft Surface 系列产品的相关特性增强。

相关特性包括且不限于以下内容：1）内核补丁（包含上游主线未同步部分），2）触摸屏，3）手写笔，4）摄像头。

## 动机

Microsoft Surface 系列产品在目前 deepin 环境下仍然支持不完善，包括且不限于 电池管理、触屏、摄像头 功能的缺失。
这些功能的缺失，在 deepin 系统安装和日常使用时，会对用户体验造成较大影响。

[linux-surface](https://github.com/linux-surface) 组织的开源工作部分弥补了这些缺陷，而相应的补丁和软件并未完全合入上游，
因此本提案希望在 deepin 系统中直接合入相关内容。


## 详细设计

- deepin kernel 需合入 `linux-surface/linux-surface` 仓库下 [对应内核版本的patches](https://github.com/linux-surface/linux-surface/tree/master/patches)；
- 增加对 linux-surface 组织中下述软件的 OBS 构建
  - [iptsd](https://github.com/linux-surface/iptsd)
  - [libwacom-surface](https://github.com/linux-surface/libwacom-surface)

## 提案弊端

N/A

## 遗留问题

- [ ] 相关 kernel patch 以何种方式加入 deepin kernel（直接并入主线，还是以 patch 形式存放）。
- [ ] 相关 kernel patch 后续如何持续保持更新，以及与 deepin kernel 主线的兼容性测试。
- [ ] 相关软件包依赖如何引导 Microsoft Surface 用户使用，是否直接在 `dde` 虚包中加入依赖。
- [ ] 需要增加 `libcamera` 和 `v4l2loopback-dkms` 软件包的OBS构建，才能支持摄像头正常使用 ([link](https://github.com/linux-surface/linux-surface/wiki/Camera-Support))。

## 替代方案

N/A

## 参考资料

1. [linux-surface - Supported Devices and Features](https://github.com/linux-surface/linux-surface/wiki/Supported-Devices-and-Features#feature-matrix)
2. [linux-surface - Compiling the Kernel from Source](https://github.com/linux-surface/linux-surface/wiki/Compiling-the-Kernel-from-Source)
3. [linux-surface - Installation and Setup](https://github.com/linux-surface/linux-surface/wiki/Installation-and-Setup#debian--ubuntu)
4. [linux-surface - Camera Support](https://github.com/linux-surface/linux-surface/wiki/Camera-Support)
