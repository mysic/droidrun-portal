# 24-Manifest 与资源系统

## 1. AndroidManifest.xml
- 作用：声明 Portal 的所有权限、组件、深链、输入法、ContentProvider、广播接收器与前台服务类型，是理解整个工程运行边界的第一入口。
- 关键内容：
  - 高权限：SYSTEM_ALERT_WINDOW、MANAGE_EXTERNAL_STORAGE、RECEIVE_SMS、READ_CONTACTS、SCHEDULE_EXACT_ALARM。
  - 核心组件：AccessibilityService、NotificationListenerService、ReverseConnectionService、ScreenCaptureService、KeepAliveService、DroidrunKeyboardIME。
  - UI 与深链：MainActivity 注册 LAUNCHER 与 droidrun://auth-callback。
  - Provider/Receiver：DroidrunContentProvider、TriggerBootReceiver、TriggerSmsReceiver、TaskPromptNotificationActionReceiver。
- 教学重点：Android 工程里，Manifest 决定“系统能不能拉起你”，而源码决定“被拉起以后做什么”。
- 证据链：[app/src/main/AndroidManifest.xml](../../app/src/main/AndroidManifest.xml)

## 2. layout 目录
- 作用：定义主界面、设置页、任务详情、任务历史、触发器规则、弹窗、列表项、自定义视图等 UI 结构。
- 关键布局：
  - activity_main.xml：主界面，包含生产模式卡片、连接信息、控制区、任务提示区。
  - activity_settings.xml：设置页，包含 local server、reverse connection、权限与 event filters。
  - view_task_prompt_card.xml / view_task_prompt_settings_panel.xml：任务提示卡片和高级设置面板。
  - activity_task_details.xml / activity_task_history.xml：任务详情与历史页面。
  - activity_trigger_rule_editor.xml / activity_trigger_rules.xml：触发器规则编辑与列表页面。
- 教学重点：UI Activity 的 Kotlin 文件负责行为，layout XML 决定页面骨架，两者必须对照着看。
- 证据链：
  - [app/src/main/res/layout/activity_main.xml](../../app/src/main/res/layout/activity_main.xml)
  - [app/src/main/res/layout/activity_settings.xml](../../app/src/main/res/layout/activity_settings.xml)

## 3. values 与主题资源
- 作用：集中管理字符串、颜色、主题与夜间主题。
- 关键文件：
  - strings.xml：几乎覆盖所有界面文案、错误提示、通知标题、按钮文本。
  - colors.xml / colors_extra.xml：定义 Portal 品牌色、状态色、任务提示 UI 色板。
  - themes.xml / values-night/themes.xml：定义 Theme.Droidrun、透明主题、Dialog 主题等。
- 教学重点：strings.xml 不只是国际化资源，也能反推出功能面；themes.xml 则直接决定 Portal 的视觉风格与控件默认样式。
- 证据链：
  - [app/src/main/res/values/strings.xml](../../app/src/main/res/values/strings.xml)
  - [app/src/main/res/values/themes.xml](../../app/src/main/res/values/themes.xml)
  - [app/src/main/res/values-night/themes.xml](../../app/src/main/res/values-night/themes.xml)

## 4. xml 目录
- 作用：放系统级 XML 配置，而不是普通界面布局。
- 关键文件：
  - accessibility_service_config.xml：声明 AccessibilityService 关心的事件类型、是否可截图、是否可手势控制。
  - method.xml：声明自定义输入法元数据。
  - backup_rules.xml / data_extraction_rules.xml：声明备份与数据导出规则。
- 教学重点：这些 XML 决定系统如何理解 Portal 的辅助功能服务与输入法，而不仅仅是“配置文件”。
- 证据链：
  - [app/src/main/res/xml/accessibility_service_config.xml](../../app/src/main/res/xml/accessibility_service_config.xml)
  - [app/src/main/res/xml/method.xml](../../app/src/main/res/xml/method.xml)

## 5. drawable 与 mipmap
- drawable：按钮背景、图标、状态标记、ripple、dialog 背景、自定义 seekbar 资源等，支撑整个 Portal UI 风格。
- mipmap：应用 launcher icon 与不同密度的启动图标资源。
- 教学重点：这些资源一般不单独承载业务逻辑，但会直接影响主题统一性、可访问性和状态反馈。

---

本文件补齐 droidrun-portal 的 Manifest 与资源系统章节，至此 app/src/main 的源码与资源目录都已纳入 analysis。