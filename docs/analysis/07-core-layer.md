# 07-Core层：StateRepository、AccessibilityTreeBuilder、JsonBuilders

## 1. StateRepository
- 作用：设备与界面状态仓库，负责 UI 元素、设备上下文、截图、输入等状态的统一获取与操作。
- 关键类/方法：StateRepository，getVisibleElements()/getFullTree()/getPhoneState()/takeScreenshot() 等。
- 调用关系：与 DroidrunAccessibilityService、AccessibilityTreeBuilder、ApiHandler 协作，驱动状态同步与自动化。
- 生命周期：随服务实例创建与销毁。
- 权限依赖：Accessibility、截图、输入等。
- 易错点：服务未激活时需降级处理，异步操作需异常捕获。
- 证据链：[app/src/main/java/com/droidrun/portal/core/StateRepository.kt](../../app/src/main/java/com/droidrun/portal/core/StateRepository.kt)

## 2. AccessibilityTreeBuilder
- 作用：辅助功能树 JSON 构建器，将 AccessibilityNodeInfo 递归转换为结构化 JSON，支持可见性过滤。
- 关键类/方法：AccessibilityTreeBuilder，buildFullAccessibilityTreeJson()。
- 调用关系：被 StateRepository 调用，驱动 UI 元素树序列化。
- 生命周期：静态工具类。
- 权限依赖：Accessibility。
- 易错点：节点递归、可见性计算、属性兼容。
- 证据链：[app/src/main/java/com/droidrun/portal/core/AccessibilityTreeBuilder.kt](../../app/src/main/java/com/droidrun/portal/core/AccessibilityTreeBuilder.kt)

## 3. JsonBuilders
- 作用：状态与元素 JSON 序列化工具，负责 ElementNode、PhoneState 等模型的结构化输出。
- 关键类/方法：JsonBuilders，elementNodeToJson()/phoneStateToJson()。
- 调用关系：被 StateRepository、ApiHandler 等调用。
- 生命周期：静态工具类。
- 权限依赖：无直接权限。
- 易错点：模型属性兼容、递归序列化。
- 证据链：[app/src/main/java/com/droidrun/portal/core/JsonBuilders.kt](../../app/src/main/java/com/droidrun/portal/core/JsonBuilders.kt)

---

本文件为 Core 层状态管理与 JSON 工具相关组件的详细讲解，后续将继续补充 API 层文件。