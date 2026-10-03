<div align="center">

# Android ID and Emulator Hider

**伪装设备身份，隐藏 root 与 Xposed，顺利通过检测。**

一款来自 [DroidRooter](https://droidrooter.com) 的 Xposed/LSPosed 模块。

[![Release](https://img.shields.io/github/v/release/saadnahid7/com.droidrooter.hider?style=for-the-badge&color=teal)](https://github.com/saadnahid7/com.droidrooter.hider/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/saadnahid7/com.droidrooter.hider/total?style=for-the-badge&color=violet)](https://github.com/saadnahid7/com.droidrooter.hider/releases)
[![Android](https://img.shields.io/badge/Android-8%20to%2016-3DDC84?style=for-the-badge&logo=android&logoColor=white)](#兼容性)
[![Xposed API](https://img.shields.io/badge/libxposed%20API-102-orange?style=for-the-badge)](https://github.com/libxposed/api)

[![DroidRooter](https://img.shields.io/badge/DroidRooter-droidrooter.com-2F6BFF?style=for-the-badge)](https://droidrooter.com)
[![Telegram](https://img.shields.io/badge/Telegram-@DroidRooter-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/DroidRooter)
[![Facebook](https://img.shields.io/badge/Facebook-DroidRooter-1877F2?style=for-the-badge&logo=facebook&logoColor=white)](https://www.facebook.com/droidrooter)

**阅读其他语言版本：** [English](README.md) · [Español](README.es.md) · [العربية](README.ar.md) · [Deutsch](README.de.md) · [日本語](README.ja.md) · [Français](README.fr.md) · [Italiano](README.it.md)

</div>

---

## 为什么选择 Android ID and Emulator Hider

许多应用一旦判断设备是模拟器、已 root 或正在运行 hook 框架，就会直接拒绝
运行，或悄悄限制自身功能。本模块会在 Java 层和 native 层同时修改这些检测
所看到的内容，让应用的表现如同运行在一台未经改动的出厂设备上一样。

- 可从 **12 种真实设备配置**（Pixel、Galaxy、POCO、OnePlus、Redmi、
  Nothing）中选择，每一种都基于经过 GSMA 验证的 IMEI 分配号段和真实的出厂
  构建指纹，而非凭空捏造的数值。
- 可按应用单独开关每一项防护，全部操作都在同一个界面完成。
- 运行 **Device Check**（设备检测），实时查看检测类应用此刻能从你的设备
  上读取到的确切信息。

基础伪装功能永久免费。一次性购买即可解锁自定义配置、安全模式以及若干额外
标识符 — 详见应用内的 **Unlock Pro（解锁高级版）**。

## 覆盖范围

| 防护项 | 具体改动 |
|---|---|
| 设备身份 | 型号、品牌、制造商、指纹（fingerprint）、构建属性、Android ID、序列号 |
| 模拟器痕迹 | qemu/goldfish 相关属性、文件、内核驱动名称、`/proc/mounts` |
| 处理器 | ABI 列表、`os.arch`，以及 `/proc/cpuinfo` 中原始的厂商/型号字符串（x86 主机） |
| 图形 | GPU 厂商及渲染器字符串 |
| 传感器 | 传感器名称及厂商 |
| 电池 | 电量、健康状态、状态、容量、sysfs 数值 |
| 输入设备 | 设备名称、`/proc/bus/input/devices` |
| 电话射频 | IMEI、IMSI、SIM 运营商/国家、号码、基带版本 |
| 摄像头 | 摄像头数量及朝向（前置/后置），按摄像头 ID 区分 |
| 位置 | 为查询最后已知位置却得不到结果的应用提供回退值 |
| Root | `su`、Magisk、KernelSU 及相关二进制文件/路径；`ro.debuggable`/`ro.secure` |
| Xposed | `/proc/self/maps`、包管理器、logcat 中的 LSPosed/Vector 痕迹 |

## 使用要求

- 一台已 root 的设备，安装有支持现代 **libxposed API 102** 的 LSPosed
  兼容框架，例如 [LSPosed](https://github.com/LSPosed/LSPosed) 或
  [Vector](https://github.com/JingMatrix/Vector)。
- Android 8.0 或更高版本。

> [!IMPORTANT]
> 本模块基于现代 libxposed API 构建，不支持传统 Xposed 及 EdXposed。

## 安装步骤

1. 从 [Releases](../../releases/latest) 下载最新 APK 并安装。
2. 打开你的 Xposed 管理器，启用 **Android ID and Emulator Hider**，并将其
   加入作用域（scope）— **它需要将自身也加入作用域**，才能保护自己的
   Device Check 界面，此外还需加入你想保护的其他应用。
3. 对每个加入作用域的应用执行强制停止，然后重新打开。

## 使用方法

1. 打开应用。一旦框架成功 hook 该进程，顶部状态卡片会显示 **Protected**。
2. 选择一个设备配置 — Pixel 8、Galaxy S24、POCO X3 Pro 以及其他九种。
3. 在 **Protection** 下分别开关各项防护功能。
4. 点击 **Device Check**，实时查看检测类应用会读取到的确切内容 — 构建
   属性、指纹、CPU、传感器、电池 — 并与当前激活的配置进行对比。

## 兼容性

| Android 版本 | API | 状态 |
|---|---|---|
| 16 | 36 | 已在真机上验证 |
| 15 | 35 | 已在真机上验证 |
| 14 | 34 | 已在真机和模拟器上验证 |
| 13 | 33 | 已在真机上验证 |
| 12 及以下 | 31 及以下 | 支持（最低 minSdk 26），未单独验证 |

"已验证"意味着该模块在开发期间已在对应 Android 版本上完成安装、加入作用
域，并确认处于正常工作状态（hook 生效、无崩溃）。

## 常见问题

**这个模块是让真机看起来像模拟器，还是让模拟器看起来像真机？**
两者皆可。伪装基于身份而非运行环境 — 无论底层实际运行的是什么，它都会改变
Java/native API 所报告的内容。

**这能绕过 Play Integrity 或 SafetyNet 吗？**
不能。硬件认证（hardware attestation）依赖设备的 TEE/StrongBox 安全芯片，
用户空间的 Xposed hook 根本无法触及 — 这需要完全不同的专门方案。

**为什么需要把应用自身也加入作用域？**
如果不这样做，应用自身的进程永远不会被 hook，因此它的 Device Check 界面
会显示设备的真实信息，而不是当前激活配置的信息 — 这会导致本该用来验证
伪装效果的唯一功能反而给出错误的结果。

**可以使用与手机真实硬件不符的配置吗（比如在 x86 模拟器上使用 ARM
配置）？**
可以 — 每个配置都会伪装处理器信息，因此 Build.SUPPORTED_ABIS、`os.arch`
以及 `/proc/cpuinfo` 中原始的厂商字符串都会切换为配置所对应的内容，而非
主机本身的信息。

## 限制

- 任何不经过被 hook 的 Java/native API 的内容 — 原始 socket 通信、服务端
  检测、硬件认证 — 看到的仍是真实设备信息。
- 修改仅在受保护应用下次启动时生效；已在运行中的应用需要重启。
- 本仓库仅托管发行版本，源代码不公开。

## 免责声明

本模块旨在用于隐私保护、测试以及与你自己开发的应用兼容。使用方式由你自行
负责。请勿用它来违反应用的使用条款、绕过付费服务，或对他人进行欺诈。本
软件按原样提供，不附带任何担保。

## 致谢

- 感谢 [libxposed](https://github.com/libxposed) 提供现代 Xposed API 及
  服务库。
- 感谢 [LSPosed](https://github.com/LSPosed/LSPosed) 与
  [Vector](https://github.com/JingMatrix/Vector) 提供运行所依赖的框架。

## 来自 DroidRooter

Android ID and Emulator Hider 是 **DroidRooter** 的一个项目，这是一支为
已 root 的 Android 设备打造工具的小团队。

- **官网：** [droidrooter.com](https://droidrooter.com)
- **Telegram：** [@DroidRooter](https://t.me/DroidRooter)
- **Facebook：** [facebook.com/droidrooter](https://www.facebook.com/droidrooter)
- **DRVCAM，DroidRooter 的虚拟摄像头：**
  [droidrooter.com/drvcam](https://www.droidrooter.com/drvcam/) 可将你自己
  的视频或图片替代摄像头画面提供给应用。
- **VirtualNet，DroidRooter 按应用进行网络伪装的工具：**
  可更改应用所获知的 Wi-Fi/移动网络连接信息，开源项目。
- **Smali Patcher Reborn：** 直接在设备上（Magisk/KernelSU/APatch）修补
  ROM 的 `services.jar`，支持模拟定位与安全窗口，适用于 Android 10–17 —
  Smali Patcher / SmaliPatcherEx 的继任者。

如果这款应用对你有帮助，欢迎关注 DroidRooter 获取更多内容。

## 许可

专有软件 — 保留所有权利。仅提供二进制分发；源代码不公开。
