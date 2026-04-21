# 20-KeepAlive 模块讲解

## 1. KeepAliveService 及相关类
- 作用：实现应用/服务的保活机制，防止被系统杀死，支持前台服务、策略切换、恢复流程等。
- 关键类/方法：KeepAliveService（前台服务）、KeepAliveController（保活控制器）、KeepAliveRecoveryActivity（恢复界面）、KeepAliveStatus/KeepAliveProcessSession/KeepAliveRecoveryPolicy 等。
- 调用关系：与 MainActivity、ReverseConnectionService、ScreenCaptureService 等协作，保证关键服务持续运行。
- 生命周期：随应用或服务启动与销毁，部分策略依赖系统事件。
- 权限依赖：FOREGROUND_SERVICE、WAKE_LOCK、相关系统权限。
- 易错点：不同 Android 版本兼容、前台服务通知、恢复策略切换。
- 证据链：
  - [app/src/main/java/com/droidrun/portal/keepalive/KeepAliveService.kt](../../app/src/main/java/com/droidrun/portal/keepalive/KeepAliveService.kt)
  - [app/src/main/java/com/droidrun/portal/keepalive/KeepAliveController.kt](../../app/src/main/java/com/droidrun/portal/keepalive/KeepAliveController.kt)
  - [app/src/main/java/com/droidrun/portal/keepalive/KeepAliveRecoveryActivity.kt](../../app/src/main/java/com/droidrun/portal/keepalive/KeepAliveRecoveryActivity.kt)
  - 其余策略与状态类见 keepalive 目录

---

本文件为 droidrun-portal 保活模块的详细讲解，补全系统级服务持续运行的关键支撑。