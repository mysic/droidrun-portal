# 02-UI层：SettingsActivity 与 TaskPrompt 相关组件

## 1. SettingsActivity
- 作用：应用设置界面，负责配置管理、权限开关、服务器与WebSocket设置、反向连接、自动化与事件过滤等。
- 关键类/方法：SettingsActivity : AppCompatActivity, ConfigManager.ConfigChangeListener；onCreate() 初始化各设置项，onResume() 同步权限与配置。
- 调用关系：ConfigManager 管理配置，PortalServiceClient 处理服务端交互，KeepAliveController 控制保活，DroidrunNotificationListener/ReverseConnectionService 相关服务。
- 生命周期：标准Activity生命周期，需处理权限动态申请与配置同步。
- 权限依赖：通知、悬浮窗、存储、网络等多项权限。
- 易错点：权限动态申请流程复杂，配置变更需及时同步到界面。
- 证据链：[app/src/main/java/com/droidrun/portal/ui/settings/SettingsActivity.kt](../../app/src/main/java/com/droidrun/portal/ui/settings/SettingsActivity.kt)

## 2. TaskPromptCardController
- 作用：任务卡片UI控制器，负责任务输入、状态展示、提交/取消、历史与详情跳转等。
- 关键类/方法：TaskPromptCardController，内部 TaskStateViewModel、StatusKind 枚举，onSubmit/onCancelTask/onOpenTaskDetails/onOpenTaskHistory 回调。
- 调用关系：与 PortalTaskDraft、PortalTaskSettings、PortalModelOption 等业务模型交互，驱动任务流 UI。
- 生命周期：依附于主界面或任务面板，随界面创建与销毁。
- 权限依赖：无直接权限，但依赖任务相关服务权限。
- 易错点：任务状态切换、按钮可用性、输入校验需细致处理。
- 证据链：[app/src/main/java/com/droidrun/portal/ui/taskprompt/TaskPromptCardController.kt](../../app/src/main/java/com/droidrun/portal/ui/taskprompt/TaskPromptCardController.kt)

## 3. TaskDetailsActivity
- 作用：任务详情界面，展示任务执行轨迹、截图、状态、错误等详细信息。
- 关键类/方法：TaskDetailsActivity : AppCompatActivity，createIntent() 工厂方法，GalleryPreviewItem 数据结构。
- 调用关系：PortalServiceClient 获取任务详情，OkHttpClient 拉取截图，PortalTaskTrajectoryUiSupport/PortalTaskScreenshotUiSupport 辅助展示。
- 生命周期：标准Activity生命周期，需处理异步加载与UI状态切换。
- 权限依赖：网络、存储（截图下载）。
- 易错点：异步加载、图片缓存、错误处理、UI状态切换。
- 证据链：[app/src/main/java/com/droidrun/portal/ui/taskprompt/TaskDetailsActivity.kt](../../app/src/main/java/com/droidrun/portal/ui/taskprompt/TaskDetailsActivity.kt)

---

本文件为 UI 层设置与任务相关组件的详细讲解，后续将继续补充 UI 及其他层文件。