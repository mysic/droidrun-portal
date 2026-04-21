# 00-项目总览与架构分层

## 1. 组件清单与权限（证据链：AndroidManifest.xml）
- Activity：MainActivity、ScreenCaptureActivity、SettingsActivity、TaskPrompt/TriggerRules相关Activity等
- Service：DroidrunAccessibilityService、DroidrunNotificationListener、ScreenCaptureService、ReverseConnectionService、KeepAliveService等
- Application：PortalApplication
- 权限：SYSTEM_ALERT_WINDOW、MANAGE_EXTERNAL_STORAGE、INTERNET、RECEIVE_BOOT_COMPLETED、RECEIVE_SMS、READ_CONTACTS、WAKE_LOCK、FOREGROUND_SERVICE等

## 2. 构建依赖与工程结构（证据链：build.gradle.kts、settings.gradle.kts、libs.versions.toml）
- 依赖集中管理，Kotlin/AndroidX/Material/OkHttp/WebRTC等
- 工程分层：UI、Service、Trigger、Streaming、Core、API

## 3. 架构分层与主链路
- UI层：界面与交互（MainActivity、ScreenCaptureActivity等）
- Service层：服务与自动化核心（DroidrunAccessibilityService、ActionDispatcher等）
- Trigger层：触发与调度（TriggerAlarmReceiver、TriggerScheduler等）
- Streaming层：流媒体与远程控制（WebRtcManager、ScrcpyControlChannel）
- Core层：核心数据与工具（StateRepository、AccessibilityTreeBuilder等）
- API层：本地API与协议（ApiHandler、ApiResponse）

### 主执行链路
1. 应用启动（MainActivity）
2. 权限与服务拉起（动态权限、服务启动）
3. Socket/API接入（SocketServer、ApiHandler）
4. Action分发（ActionDispatcher）
5. Accessibility执行（DroidrunAccessibilityService）
6. 状态回传（WebSocket、API、事件）

### 状态/数据流
- 命令输入：SocketServer、ApiHandler
- 事件总线：Trigger层调度
- 序列化消息：JsonBuilders、ApiResponse
- 设备状态存储：StateRepository

---

本文件为 droidrun-portal 教学分析的总览与分层架构部分，所有结论均附证据链，便于复查。