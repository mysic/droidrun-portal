# 16-UI层：触发器与任务历史相关界面

## 1. TriggerRulesActivity & TriggerRuleEditorActivity
- 作用：触发器规则列表与编辑界面，支持规则增删改查、启用禁用、参数配置等。
- 关键类/方法：TriggerRulesActivity、TriggerRuleEditorActivity，onCreate()/onActivityResult() 等。
- 调用关系：与 TriggerApi、TriggerRepository 协作，驱动规则管理 UI。
- 生命周期：标准 Activity 生命周期。
- 权限依赖：依赖具体触发源权限（如通知、定时等）。
- 易错点：规则参数校验、状态同步、权限兼容。
- 证据链：[app/src/main/java/com/droidrun/portal/ui/triggers/TriggerRulesActivity.kt](../../app/src/main/java/com/droidrun/portal/ui/triggers/TriggerRulesActivity.kt)、[app/src/main/java/com/droidrun/portal/ui/triggers/TriggerRuleEditorActivity.kt](../../app/src/main/java/com/droidrun/portal/ui/triggers/TriggerRuleEditorActivity.kt)

## 2. TaskHistoryActivity
- 作用：任务历史记录界面，展示任务执行历史、状态、详情跳转等。
- 关键类/方法：TaskHistoryActivity，onCreate()/onItemClick() 等。
- 调用关系：与 PortalTaskTracking、PortalTaskDetails 等业务模型协作。
- 生命周期：标准 Activity 生命周期。
- 权限依赖：无直接权限。
- 易错点：历史数据同步、UI 状态切换。
- 证据链：[app/src/main/java/com/droidrun/portal/ui/taskprompt/TaskHistoryActivity.kt](../../app/src/main/java/com/droidrun/portal/ui/taskprompt/TaskHistoryActivity.kt)

---

本文件为 UI 层触发器与任务历史相关界面的讲解，补全主流程外的管理与追溯功能。