# 10-Kotlin/Android 语法与机制教学实例

## 1. Kotlin 语法实例
- data class：如 TriggerRule、PortalTaskDetails 等，简化数据结构定义，自动生成 equals/hashCode/toString。
- sealed class：如 ApiResponse，表达有限状态集合，类型安全。
- 扩展函数：如 elementNodeToJson()，为已有类型添加新功能。
- 协程与 suspend：部分异步操作采用 CompletableFuture 或 suspend 函数，便于并发与回调简化。
- Flow/StateFlow：如有使用，适合状态流转与响应式编程。

## 2. Android 关键机制
- Activity/Service/Receiver 生命周期：如 MainActivity、ScreenCaptureService、TriggerAlarmReceiver，需关注启动、销毁、权限、前台服务等。
- 权限管理：动态申请（如通知、存储、悬浮窗）、Manifest 注册、用户授权流程。
- ContentProvider：用于触发器与状态数据的本地跨进程访问。
- 前台服务与保活：如 ReverseConnectionService、ScreenCaptureService，需前台通知与权限。

## 3. 工程与依赖管理
- Gradle 依赖集中管理：libs.versions.toml，便于多模块统一升级。
- 构建变体与混淆：release 默认未混淆，便于调试。

## 4. 教学建议与易错点
- 跨语言类比：data class 类似 Python dataclass/Go struct，sealed class 类似枚举联合类型。
- 最小示例：每知识点配合真实源码片段。
- 常见坑：权限未授权、服务未保活、异步回调未处理异常、协议兼容性。
- 排错建议：日志、断点、单元测试、协议抓包。

---

本文件为 droidrun-portal 项目内常见 Kotlin/Android 语法与机制的教学实例，结合源码实际场景，便于初学者跨语言理解与实战应用。