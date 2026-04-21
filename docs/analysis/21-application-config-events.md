# 21-启动、配置与事件总线模块

## 1. PortalApplication
- 作用：应用级入口，注册 ActivityLifecycleCallbacks，跟踪前后台切换，并在应用回到前台时尝试恢复 keep-alive。
- 关键类/方法：PortalApplication，onCreate()，onAppForegrounded()，onAppBackgrounded()。
- 调用关系：依赖 AppForegroundTransitionTracker、AppVisibilityTracker、KeepAliveController。
- 生命周期：Application 级，全进程只初始化一次。
- 易错点：前后台切换逻辑不要放在单个 Activity；保活恢复要避免在后台直接拉起敏感流程。
- 证据链：[app/src/main/java/com/droidrun/portal/PortalApplication.kt](../../app/src/main/java/com/droidrun/portal/PortalApplication.kt)

## 2. ConfigManager
- 作用：全局配置中心，统一管理 SharedPreferences、设备标识、认证 token、事件开关、反向连接、任务提示、keep-alive 状态等。
- 关键类/方法：ConfigManager 单例，getInstance()，authToken，deviceID，以及各类配置读写接口。
- 调用关系：被 MainActivity、SettingsActivity、ReverseConnectionService、PortalTaskLaunchCoordinator、EventHub 等广泛依赖。
- 生命周期：应用级单例。
- 易错点：普通配置、设备配置、敏感配置被拆到不同 SharedPreferences；迁移逻辑与默认值要保持兼容。
- 证据链：[app/src/main/java/com/droidrun/portal/config/ConfigManager.kt](../../app/src/main/java/com/droidrun/portal/config/ConfigManager.kt)

## 3. EventHub、LocalDeviceEventRelay 与 PortalWebSocketServer
- 作用：事件中枢与本地 WebSocket 事件出口。EventHub 负责订阅/广播 PortalEvent；LocalDeviceEventRelay 负责把设备事件按连接能力与路由格式发给本地 WebSocket 客户端；PortalWebSocketServer 负责鉴权、接收 JSON-RPC 指令、承载本地事件流。
- 关键类/方法：EventHub.init()/subscribe()/emit()；LocalDeviceEventRelay.emit()/register()/unregister()；PortalWebSocketServer.onOpen()/onMessage()/onClose()。
- 调用关系：DroidrunNotificationListener、TriggerRuntime、ReverseDeviceEventRelay、本地 WebSocket 客户端都会经过这一层。
- 生命周期：EventHub 为进程级对象；PortalWebSocketServer 随设置或服务启动。
- 易错点：事件过滤由 ConfigManager 控制；WebSocket 既承载命令请求也承载无请求 id 的设备事件，二者不要混淆。
- 证据链：
  - [app/src/main/java/com/droidrun/portal/events/EventHub.kt](../../app/src/main/java/com/droidrun/portal/events/EventHub.kt)
  - [app/src/main/java/com/droidrun/portal/events/LocalDeviceEventRelay.kt](../../app/src/main/java/com/droidrun/portal/events/LocalDeviceEventRelay.kt)
  - [app/src/main/java/com/droidrun/portal/events/PortalWebSocketServer.kt](../../app/src/main/java/com/droidrun/portal/events/PortalWebSocketServer.kt)
  - [app/src/main/java/com/droidrun/portal/events/model/EventType.kt](../../app/src/main/java/com/droidrun/portal/events/model/EventType.kt)
  - [app/src/main/java/com/droidrun/portal/events/model/PortalEvent.kt](../../app/src/main/java/com/droidrun/portal/events/model/PortalEvent.kt)

## 4. 这层在架构里的位置
- PortalApplication 决定应用启动时的全局行为。
- ConfigManager 是所有模块共享的配置与持久化边界。
- EventHub 和 PortalWebSocketServer 组成“设备事件 -> 协议输出”的总线层。

---

本文件补齐 droidrun-portal 的启动入口、配置中心与事件总线章节。