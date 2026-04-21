# 08-API层：ApiHandler 与 ApiResponse

## 1. ApiHandler
- 作用：本地 API 处理器，负责自动化指令、状态查询、安装包管理、截图、输入等 API 的统一实现。
- 关键类/方法：ApiHandler，performTap()/performSwipe()/takeScreenshot()/inputText() 等。
- 调用关系：与 StateRepository、DroidrunAccessibilityService、ScreenCaptureService、WebRtcManager 等协作，驱动本地与远程 API。
- 生命周期：随服务或服务器实例创建与销毁。
- 权限依赖：Accessibility、存储、网络、安装包等。
- 易错点：参数校验、权限兼容、异步操作、错误处理。
- 证据链：[app/src/main/java/com/droidrun/portal/api/ApiHandler.kt](../../app/src/main/java/com/droidrun/portal/api/ApiHandler.kt)

## 2. ApiResponse
- 作用：API 响应封装，支持 Success/Error/RawObject/RawArray/Binary/Text 多种响应类型，统一序列化为 JSON。
- 关键类/方法：ApiResponse，toJson()。
- 调用关系：被 ApiHandler、ActionDispatcher、WebSocket 等调用，统一 API 返回格式。
- 生命周期：静态数据结构。
- 权限依赖：无直接权限。
- 易错点：类型兼容、序列化一致性。
- 证据链：[app/src/main/java/com/droidrun/portal/api/ApiResponse.kt](../../app/src/main/java/com/droidrun/portal/api/ApiResponse.kt)

---

本文件为 API 层本地指令与响应相关组件的详细讲解，至此已覆盖 droidrun-portal 全项目主要源码分层。