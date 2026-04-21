# 15-工具与辅助类讲解

## 1. OverlayManager（UI 层）
- 作用：负责全局悬浮层的绘制与管理，支持元素高亮、位置校正、可视化调试等。
- 关键类/方法：OverlayManager，setPositionOffsetY()/addElement()/removeElement() 等。
- 调用关系：与 MainActivity、DroidrunAccessibilityService 协作，辅助 UI 自动化与调试。
- 生命周期：随主界面或服务创建与销毁。
- 权限依赖：SYSTEM_ALERT_WINDOW（悬浮窗权限）。
- 易错点：兼容不同 Android 版本的窗口管理、坐标校正。
- 证据链：[app/src/main/java/com/droidrun/portal/ui/overlay/OverlayManager.kt](../../app/src/main/java/com/droidrun/portal/ui/overlay/OverlayManager.kt)

## 2. EditTextExtensions（UI 层）
- 作用：为 EditText 提供扩展函数，自动去除输入空白字符。
- 关键类/方法：addWhitespaceStrippingWatcher()。
- 调用关系：被 SettingsActivity、任务输入等界面调用。
- 生命周期：静态扩展函数。
- 权限依赖：无。
- 易错点：输入监听递归、光标位置处理。
- 证据链：[app/src/main/java/com/droidrun/portal/ui/EditTextExtensions.kt](../../app/src/main/java/com/droidrun/portal/ui/EditTextExtensions.kt)

## 3. GestureController（Service 层）
- 作用：统一封装手势与全局操作（点击、滑动、Home/Back 等），通过 AccessibilityService 执行。
- 关键类/方法：GestureController，tap()/swipe()/performGlobalAction()。
- 调用关系：被 ApiHandler、ActionDispatcher、ScrcpyControlChannel 等调用。
- 生命周期：静态工具类。
- 权限依赖：Accessibility。
- 易错点：手势参数、服务未激活时降级。
- 证据链：[app/src/main/java/com/droidrun/portal/service/GestureController.kt](../../app/src/main/java/com/droidrun/portal/service/GestureController.kt)

## 4. FileOperations（Service 层）
- 作用：封装文件读写、列表、删除等操作，限制于 /sdcard 目录，防止越权。
- 关键类/方法：FileOperations，resolvePath()/listFiles()/readFile()/writeFile() 等。
- 调用关系：被 ApiHandler、ActionDispatcher 等调用。
- 生命周期：随服务实例创建与销毁。
- 权限依赖：MANAGE_EXTERNAL_STORAGE、读写存储。
- 易错点：路径校验、防止目录遍历、权限兼容。
- 证据链：[app/src/main/java/com/droidrun/portal/service/FileOperations.kt](../../app/src/main/java/com/droidrun/portal/service/FileOperations.kt)

---

本文件为 droidrun-portal 项目主要工具与辅助类的讲解，补全主流程外的关键支撑模块。