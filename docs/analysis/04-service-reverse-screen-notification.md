# 04-Service层：ReverseConnectionService、ScreenCaptureService、DroidrunNotificationListener

## 1. ReverseConnectionService
- 作用：反向连接服务，设备主动连接云端 WebSocket，实现 NAT/移动网络下的远程控制与事件推送。
- 关键类/方法：ReverseConnectionService : Service，getInstance() 单例，isTerminalClose()/shouldGiveUpReconnecting() 连接管理。
- 调用关系：与 WebRtcManager、ApiHandler、EventHub、StateRepository 等协作，驱动云端指令与状态同步。
- 生命周期：前台服务，需在 Manifest 注册，随应用/用户操作启动与销毁。
- 权限依赖：INTERNET、前台服务权限。
- 易错点：断线重连、认证失效、云端协议兼容、前台服务保活。
- 证据链：[app/src/main/java/com/droidrun/portal/service/ReverseConnectionService.kt](../../app/src/main/java/com/droidrun/portal/service/ReverseConnectionService.kt)

## 2. ScreenCaptureService
- 作用：屏幕采集与投屏服务，结合 WebRtcManager 实现本地/云端屏幕流媒体推送。
- 关键类/方法：ScreenCaptureService : Service，onStartCommand() 处理权限与流媒体启动，requestStop() 停止流。
- 调用关系：与 WebRtcManager、ReverseConnectionService 协作，驱动屏幕采集与推流。
- 生命周期：前台服务，需动态权限与前台通知，随投屏需求启动与销毁。
- 权限依赖：FOREGROUND_SERVICE、MediaProjection。
- 易错点：权限申请、流媒体参数、前台服务保活、异常恢复。
- 证据链：[app/src/main/java/com/droidrun/portal/service/ScreenCaptureService.kt](../../app/src/main/java/com/droidrun/portal/service/ScreenCaptureService.kt)

## 3. DroidrunNotificationListener
- 作用：通知监听服务，捕获系统通知并转发为 Portal 事件。
- 关键类/方法：DroidrunNotificationListener : NotificationListenerService，onNotificationPosted()/onNotificationRemoved() 事件处理。
- 调用关系：与 EventHub、TriggerRuntime 协作，驱动通知事件流。
- 生命周期：系统服务，需在 Manifest 注册并动态授权，随系统调度启动与销毁。
- 权限依赖：BIND_NOTIFICATION_LISTENER_SERVICE，需用户手动授权。
- 易错点：通知权限丢失、事件格式兼容、异常处理。
- 证据链：[app/src/main/java/com/droidrun/portal/service/DroidrunNotificationListener.kt](../../app/src/main/java/com/droidrun/portal/service/DroidrunNotificationListener.kt)

---

本文件为 Service 层反向连接、屏幕采集、通知监听相关组件的详细讲解，后续将继续补充 Trigger、Streaming、Core、API 层文件。