# 01-UI层：MainActivity 与 ScreenCaptureActivity

## 1. MainActivity
- 作用：主界面，负责状态面板、任务入口、权限检查、服务拉起等
- 关键类/方法：MainActivity : AppCompatActivity, ConfigManager.ConfigChangeListener；onCreate() 初始化UI与权限
- 调用关系：ConfigManager监听配置，启动/绑定服务，ApiHandler处理本地API
- 生命周期：标准Activity生命周期，需处理权限弹窗与服务绑定
- 权限依赖：Accessibility、悬浮窗、存储等
- 易错点：权限未授权功能不可用，服务未启动时UI需反馈
- 证据链：[app/src/main/java/com/droidrun/portal/ui/MainActivity.kt](../app/src/main/java/com/droidrun/portal/ui/MainActivity.kt)

## 2. ScreenCaptureActivity
- 作用：透明Activity，用于申请屏幕投屏权限，结果回传ScreenCaptureService
- 关键类/方法：ScreenCaptureActivity : Activity；onCreate()发起权限请求，onActivityResult()处理结果
- 调用关系：由服务/调度器启动，权限结果传递给ScreenCaptureService，失败时通过ReverseConnectionService上报
- 生命周期：仅用于权限申请，结束即finish
- 权限依赖：MediaProjection
- 易错点：权限被拒绝需正确处理，参数透传需与服务端一致
- 证据链：[app/src/main/java/com/droidrun/portal/ui/ScreenCaptureActivity.kt](../app/src/main/java/com/droidrun/portal/ui/ScreenCaptureActivity.kt)

---

本文件为 UI 层主界面与投屏权限申请流程的详细讲解，后续将继续补充 UI 及其他层文件。