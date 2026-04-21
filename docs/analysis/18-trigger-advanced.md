# 18-Trigger层：高级与辅助模块

## 1. TriggerModels/TriggerMatcher/TriggerRuleValidator/TriggerTemplateRenderer
- 作用：触发器数据模型、规则匹配、参数校验、模板渲染等底层支撑。
- 关键类/方法：TriggerModels（数据结构）、TriggerMatcher（规则匹配）、TriggerRuleValidator（参数校验）、TriggerTemplateRenderer（模板渲染）。
- 调用关系：被 TriggerApi、TriggerRuntime、TriggerRepository 等调用。
- 生命周期：静态工具类或数据结构。
- 权限依赖：依赖具体触发源权限。
- 易错点：规则表达式、模板语法、参数校验。
- 证据链：[app/src/main/java/com/droidrun/portal/triggers/TriggerModels.kt](../../app/src/main/java/com/droidrun/portal/triggers/TriggerModels.kt)、[app/src/main/java/com/droidrun/portal/triggers/TriggerMatcher.kt](../../app/src/main/java/com/droidrun/portal/triggers/TriggerMatcher.kt)、[app/src/main/java/com/droidrun/portal/triggers/TriggerRuleValidator.kt](../../app/src/main/java/com/droidrun/portal/triggers/TriggerRuleValidator.kt)、[app/src/main/java/com/droidrun/portal/triggers/TriggerTemplateRenderer.kt](../../app/src/main/java/com/droidrun/portal/triggers/TriggerTemplateRenderer.kt)

## 2. TriggerTaskLauncher/TriggerUiSupport/TriggerEditorSupport/TriggerTimeSupport/TriggerSmsReceiver/TriggerScheduler/TriggerBootReceiver
- 作用：任务调度、UI 支持、编辑器辅助、时间与短信触发、定时与开机广播等。
- 关键类/方法：TriggerTaskLauncher、TriggerUiSupport、TriggerEditorSupport、TriggerTimeSupport、TriggerSmsReceiver、TriggerScheduler、TriggerBootReceiver。
- 调用关系：与 TriggerRuntime、TriggerRepository、EventHub 协作。
- 生命周期：随应用或服务启动与销毁。
- 权限依赖：定时、短信、开机等权限。
- 易错点：广播注册、权限兼容、调度精度。
- 证据链：相关文件均在 triggers 目录下。

---

本文件为 Trigger 层高级与辅助模块讲解，补全主流程外的规则表达、调度与集成支撑。