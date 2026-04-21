# 19-UI层：剩余辅助与对话界面

## 1. PermissionDialogActivity
- 作用：权限弹窗界面，辅助动态权限申请与用户交互。
- 关键类/方法：PermissionDialogActivity，onCreate()/onRequestPermissionsResult()。
- 调用关系：与 MainActivity、SettingsActivity 协作。
- 生命周期：标准 Activity 生命周期。
- 权限依赖：依赖具体权限（如存储、通知等）。
- 易错点：权限回调、用户拒绝处理。
- 证据链：[app/src/main/java/com/droidrun/portal/ui/PermissionDialogActivity.kt](../../app/src/main/java/com/droidrun/portal/ui/PermissionDialogActivity.kt)

## 2. TaskPromptSettingsPanelController
- 作用：任务提示设置面板控制器，管理任务输入相关设置。
- 关键类/方法：TaskPromptSettingsPanelController。
- 调用关系：与 TaskPromptCardController、SettingsActivity 协作。
- 生命周期：随主界面或任务面板创建与销毁。
- 权限依赖：无直接权限。
- 易错点：设置同步、UI 状态切换。
- 证据链：[app/src/main/java/com/droidrun/portal/ui/taskprompt/TaskPromptSettingsPanelController.kt](../../app/src/main/java/com/droidrun/portal/ui/taskprompt/TaskPromptSettingsPanelController.kt)

---

本文件为 UI 层剩余辅助与对话界面的讲解，至此已覆盖全部主流程与辅助模块。