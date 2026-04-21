# 22-输入法、模型与状态模块

## 1. DroidrunKeyboardIME
- 作用：自定义输入法服务，为自动化输入提供稳定入口，支持直接输入文本、Base64 文本、清空输入框、发送按键事件。
- 关键类/方法：DroidrunKeyboardIME，inputB64Text()，inputText()，clearText()，sendKeyEventDirect()，isSelected()。
- 调用关系：被 ApiHandler、DroidrunAccessibilityService、ScrcpyControlChannel 等调用。
- 生命周期：InputMethodService，由系统根据输入法激活状态创建。
- 权限依赖：BIND_INPUT_METHOD；还依赖用户将该输入法设为默认或至少可切换。
- 易错点：IME 已安装不代表正在选中；currentInputConnection 为空时所有输入能力都会失败。
- 证据链：[app/src/main/java/com/droidrun/portal/input/DroidrunKeyboardIME.kt](../../app/src/main/java/com/droidrun/portal/input/DroidrunKeyboardIME.kt)

## 2. model 包
- 作用：承载 Portal 在自动化与文件系统中的基础数据模型，如 ElementNode、PhoneState、FileInfo。
- 关键模型：
  - ElementNode：表示可见 UI 元素，带 Rect、层级、父子关系、点击索引等信息。
  - PhoneState：表示当前前台应用、焦点元素、键盘可见性等状态。
  - FileInfo/FilePermissions/FileType：描述文件浏览与文件操作结果。
- 调用关系：被 AccessibilityService、StateRepository、JsonBuilders、FileOperations 调用。
- 易错点：ElementNode 持有 AccessibilityNodeInfo，构建与释放要注意生命周期；模型字段既服务 UI，也服务 API 序列化。
- 证据链：[app/src/main/java/com/droidrun/portal/model/ElementNode.kt](../../app/src/main/java/com/droidrun/portal/model/ElementNode.kt)

## 3. state 包
- 作用：承载 Portal 的运行时状态与应用可见性状态，包括连接状态、前后台状态与应用切换跟踪。
- 关键类/方法：
  - ConnectionStateManager：对外暴露 LiveData 连接状态。
  - AppVisibilityTracker：记录进程是否处于前台。
  - AppForegroundTransitionTracker：根据 Activity start/stop 统计前后台转换。
  - AppVisibilityTracker：为 keep-alive、任务完成回跳等逻辑提供条件判断。
- 调用关系：被 PortalApplication、MainActivity、SettingsActivity、ReverseConnectionService 等调用。
- 易错点：连接状态可能由后台线程更新，所以这里使用 postValue；前后台状态和网络连接状态不是一回事。
- 证据链：
  - [app/src/main/java/com/droidrun/portal/state/ConnectionStateManager.kt](../../app/src/main/java/com/droidrun/portal/state/ConnectionStateManager.kt)
  - [app/src/main/java/com/droidrun/portal/state/AppVisibilityTracker.kt](../../app/src/main/java/com/droidrun/portal/state/AppVisibilityTracker.kt)
  - [app/src/main/java/com/droidrun/portal/state/AppForegroundTransitionTracker.kt](../../app/src/main/java/com/droidrun/portal/state/AppForegroundTransitionTracker.kt)

## 4. 学习重点
- 这层把“系统能力”抽成可复用的数据与状态，不直接操作 UI。
- 初学者应先理解：输入法服务是输入边界，model 是数据边界，state 是运行时状态边界。

---

本文件补齐 droidrun-portal 的输入法、基础模型与状态管理章节。