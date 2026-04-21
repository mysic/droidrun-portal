# 03-Service层：DroidrunAccessibilityService、ActionDispatcher、SocketServer

## 1. DroidrunAccessibilityService
- 作用：核心自动化服务，实现 AccessibilityService，负责 UI 元素遍历、自动化操作、事件监听、状态同步等。
- 关键类/方法：DroidrunAccessibilityService : AccessibilityService, ConfigManager.ConfigChangeListener；onAccessibilityEvent() 处理事件，calculateInputText() 输入文本处理。
- 调用关系：与 StateRepository、ApiHandler、OverlayManager、EventHub、PortalWebSocketServer 等协作，驱动自动化与状态同步。
- 生命周期：系统服务，需在 Manifest 注册并动态授权，随系统调度启动与销毁。
- 权限依赖：BIND_ACCESSIBILITY_SERVICE，需用户手动授权。
- 易错点：事件处理高频，需防止死循环与性能瓶颈；权限丢失时需降级处理。
- 证据链：[app/src/main/java/com/droidrun/portal/service/DroidrunAccessibilityService.kt](../../app/src/main/java/com/droidrun/portal/service/DroidrunAccessibilityService.kt)

## 2. ActionDispatcher
- 作用：指令分发枢纽，统一处理 tap、swipe 等自动化动作，支持 HTTP、WebSocket、Reverse 三种来源。
- 关键类/方法：ActionDispatcher，dispatch() 方法根据 action/params 分发到 ApiHandler、TriggerApi。
- 调用关系：被 SocketServer、PortalWebSocketServer 等调用，底层依赖 ApiHandler、TriggerApi。
- 生命周期：随服务或服务器实例创建与销毁。
- 权限依赖：依赖具体动作所需权限（如 Accessibility、触摸、输入等）。
- 易错点：参数校验、动作归一化、异常处理需健全，防止误操作。
- 证据链：[app/src/main/java/com/droidrun/portal/service/ActionDispatcher.kt](../../app/src/main/java/com/droidrun/portal/service/ActionDispatcher.kt)

## 3. SocketServer
- 作用：本地 HTTP/WebSocket 服务器，负责接收外部指令、认证、分发到 ActionDispatcher。
- 关键类/方法：SocketServer，start()/stop() 控制服务，acceptConnections() 处理连接。
- 调用关系：依赖 ApiHandler、ConfigManager、ActionDispatcher，驱动本地自动化与 API。
- 生命周期：随应用或服务启动/关闭，支持多线程并发。
- 权限依赖：INTERNET、本地网络、认证 token。
- 易错点：端口占用、认证校验、并发处理、异常恢复。
- 证据链：[app/src/main/java/com/droidrun/portal/service/SocketServer.kt](../../app/src/main/java/com/droidrun/portal/service/SocketServer.kt)

---

本文件为 Service 层核心自动化与指令分发相关组件的详细讲解，后续将继续补充 Service 及其他层文件。