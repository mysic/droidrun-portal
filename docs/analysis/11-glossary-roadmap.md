# 11-术语表与学习路线图

## 1. 术语表
- AccessibilityService：Android 辅助功能服务，支持自动化 UI 操作。
- Foreground Service：前台服务，需常驻通知，保证进程存活。
- BroadcastReceiver：广播接收器，响应系统或应用事件。
- Reverse Connection：反向连接，设备主动连接云端实现 NAT 穿透。
- WebRTC：实时音视频通信协议，支持屏幕投屏与远程控制。
- ContentProvider：Android 跨进程数据访问机制。
- DataChannel：WebRTC 数据通道，支持远程控制指令。
- Trigger/Rule：自动化触发器与规则，支持定时、事件、通知等多种触发源。
- StateRepository：设备与界面状态仓库，统一管理状态。
- ApiHandler：本地 API 处理器，统一自动化与状态查询接口。

## 2. 学习路线图
1. 先读 AndroidManifest.xml，理解组件与权限总表。
2. 阅读 MainActivity、SettingsActivity，掌握主界面与配置管理。
3. 理解 Service 层核心服务（DroidrunAccessibilityService、ReverseConnectionService、ScreenCaptureService）。
4. 掌握 Trigger 层触发器管理与事件调度机制。
5. 理解 Streaming 层 WebRTC 投屏与远程控制实现。
6. 熟悉 Core 层状态管理与 JSON 工具。
7. 理解 API 层本地指令与协议响应。
8. 结合协议文档，掌握 WebSocket、本地 API、反向连接、触发器协议。
9. 穿插学习 Kotlin/Android 语法与工程机制，结合真实源码实例。
10. 参考术语表，查阅不熟悉的关键概念。

---

本文件为 droidrun-portal 项目术语表与推荐学习路线，便于初学者系统掌握全项目架构与关键知识点。