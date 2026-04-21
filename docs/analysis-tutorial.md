# droidrun-portal 全项目源码教学教程

---

## 1. 项目总览与分层

### 1.1 组件清单与权限（证据链：AndroidManifest.xml）
- Activity：MainActivity、ScreenCaptureActivity、SettingsActivity、TaskPrompt/TriggerRules相关Activity等
- Service：DroidrunAccessibilityService、DroidrunNotificationListener、ScreenCaptureService、ReverseConnectionService、KeepAliveService等
- Application：PortalApplication
- 权限：SYSTEM_ALERT_WINDOW、MANAGE_EXTERNAL_STORAGE、INTERNET、RECEIVE_BOOT_COMPLETED、RECEIVE_SMS、READ_CONTACTS、WAKE_LOCK、FOREGROUND_SERVICE等

### 1.2 构建依赖与工程结构（证据链：build.gradle.kts、settings.gradle.kts、libs.versions.toml）
- 依赖集中管理，Kotlin/AndroidX/Material/OkHttp/WebRTC等
- 工程分层：UI、Service、Trigger、Streaming、Core、API

### 1.3 架构分层与主链路
- UI层：界面与交互（MainActivity、ScreenCaptureActivity等）
- Service层：服务与自动化核心（DroidrunAccessibilityService、ActionDispatcher等）
- Trigger层：触发与调度（TriggerAlarmReceiver、TriggerScheduler等）
- Streaming层：流媒体与远程控制（WebRtcManager、ScrcpyControlChannel）
- Core层：核心数据与工具（StateRepository、AccessibilityTreeBuilder等）
- API层：本地API与协议（ApiHandler、ApiResponse）

#### 主执行链路
1. 应用启动（MainActivity）
2. 权限与服务拉起（动态权限、服务启动）
3. Socket/API接入（SocketServer、ApiHandler）
4. Action分发（ActionDispatcher）
5. Accessibility执行（DroidrunAccessibilityService）
6. 状态回传（WebSocket、API、事件）

#### 状态/数据流
- 命令输入：SocketServer、ApiHandler
- 事件总线：Trigger层调度
- 序列化消息：JsonBuilders、ApiResponse
- 设备状态存储：StateRepository

---

## 2. UI层文件讲解（示例）

### 2.1 MainActivity
- 作用：主界面，负责状态面板、任务入口、权限检查、服务拉起等
- 关键类/方法：MainActivity : AppCompatActivity, ConfigManager.ConfigChangeListener；onCreate() 初始化UI与权限
- 调用关系：ConfigManager监听配置，启动/绑定服务，ApiHandler处理本地API
- 生命周期：标准Activity生命周期，需处理权限弹窗与服务绑定
- 权限依赖：Accessibility、悬浮窗、存储等
- 易错点：权限未授权功能不可用，服务未启动时UI需反馈
- 证据链：[app/src/main/java/com/droidrun/portal/ui/MainActivity.kt](../app/src/main/java/com/droidrun/portal/ui/MainActivity.kt)

### 2.2 ScreenCaptureActivity
- 作用：透明Activity，用于申请屏幕投屏权限，结果回传ScreenCaptureService
- 关键类/方法：ScreenCaptureActivity : Activity；onCreate()发起权限请求，onActivityResult()处理结果
- 调用关系：由服务/调度器启动，权限结果传递给ScreenCaptureService，失败时通过ReverseConnectionService上报
- 生命周期：仅用于权限申请，结束即finish
- 权限依赖：MediaProjection
- 易错点：权限被拒绝需正确处理，参数透传需与服务端一致
- 证据链：[app/src/main/java/com/droidrun/portal/ui/ScreenCaptureActivity.kt](../app/src/main/java/com/droidrun/portal/ui/ScreenCaptureActivity.kt)

---

## 3. 协议与事件机制（概览）

### 3.1 WebSocket事件
- 事件类型：NOTIFICATION、APP_ENTERED、BATTERY_LOW、USER_PRESENT、NETWORK_CONNECTED、SMS_RECEIVED等
- 事件格式：{"type": "EVENT_TYPE", "timestamp": ..., "payload": {...}}
- 支持JSON-RPC风格命令，详见 local-api.md
- 证据链：[docs/websocket-events.md](websocket-events.md)

### 3.2 本地API与反向连接
- 支持HTTP/WebSocket/ContentProvider本地控制，需token认证
- 方法示例：tap、swipe、global、app、keyboard/input、screenshot、packages、state、install等
- 反向连接（云控）：设备主动连接云端，协议与本地一致，支持事件推送与触发器管理
- 证据链：[docs/local-api.md](local-api.md)、[docs/reverse-connection.md](reverse-connection.md)

### 3.3 触发器与事件管理
- 支持触发器增删改查、启用禁用、测试、运行记录等
- 统一TriggerJson schema，接口支持本地与云端
- 证据链：[docs/triggers.md](triggers.md)

---

## 4. Kotlin/Android 教学联动（后续分批补充）
- 结合源码实例，讲解Kotlin语法（data class、协程、扩展函数等）与Android机制（Service、权限、ContentProvider）
- 每知识点给“跨语言类比 + 最小示例 + 易错提醒”

---

## 5. 已覆盖/未覆盖清单与下一步计划
- 已覆盖：项目分层、主链路、MainActivity、ScreenCaptureActivity、协议文档概览
- 未覆盖：UI层其余文件、Service/Trigger/Streaming/Core/API层详细讲解、Kotlin/Android知识点实例
- 下一步：继续分批讲解各层文件，穿插协议与语法教学，完善教程内容

---

本教程持续迭代，所有结论均附证据链，便于复查与扩展。