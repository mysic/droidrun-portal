# 23-taskprompt 业务域模块

## 1. PortalServiceClient
- 作用：对接 Portal 主机侧任务服务接口，负责模型列表、余额、任务启动、任务详情、轨迹、截图、取消等 HTTP 交互。
- 关键类/方法：PortalServiceClient，fallbackModelOptions()，deriveRestBaseUrl()，deriveBillingBaseUrl() 以及各类 task/balance/models 请求。
- 调用关系：被 MainActivity、SettingsActivity、TaskDetailsActivity、TaskHistoryActivity、PortalTaskLaunchCoordinator 等调用。
- 生命周期：通常随页面控制器或业务服务创建。
- 易错点：Reverse WebSocket URL 会被换算成 REST base URL；模型列表支持回退；HTTP 错误要区分硬失败与可重试失败。
- 证据链：[app/src/main/java/com/droidrun/portal/taskprompt/PortalServiceClient.kt](../../app/src/main/java/com/droidrun/portal/taskprompt/PortalServiceClient.kt)

## 2. PortalTaskLaunchCoordinator
- 作用：任务启动编排器，负责在本地校验 API key、URL、活跃任务状态，再调用服务端启动任务，并把返回结果写入 ConfigManager 与通知系统。
- 关键类/方法：launchPrompt()，buildActiveTaskRecord()。
- 调用关系：依赖 ConfigManager、PortalServiceClient、TaskPromptNotificationManager、PortalTaskStateMonitor。
- 易错点：这里既做了启动前校验，也做了启动后本地状态落库；如果只看 UI 控件，很容易漏掉这层真正的业务编排。
- 证据链：[app/src/main/java/com/droidrun/portal/taskprompt/PortalTaskLaunchCoordinator.kt](../../app/src/main/java/com/droidrun/portal/taskprompt/PortalTaskLaunchCoordinator.kt)

## 3. PortalTaskTracking 与相关数据结构
- 作用：定义任务记录、任务历史、详情、截图、状态机与状态辅助函数，是 taskprompt 子系统的数据与状态判断核心。
- 关键类/方法：
  - PortalActiveTaskRecord、PortalTaskHistoryItem、PortalTaskDetails、PortalTaskScreenshotSet。
  - PortalTaskTracking.computePollDeadline()、isTerminalStatus()、isBlockingStatus()、withUpdatedStatus()。
- 调用关系：被 ConfigManager、PortalTaskLaunchCoordinator、PortalTaskStateMonitor、TaskPromptNotificationManager、UI 层多个 Activity/Controller 调用。
- 易错点：本地状态与服务端状态并不完全相同，PortalTaskTracking 额外引入了 tracking_timeout 等本地状态。
- 证据链：[app/src/main/java/com/droidrun/portal/taskprompt/PortalTaskTracking.kt](../../app/src/main/java/com/droidrun/portal/taskprompt/PortalTaskTracking.kt)

## 4. taskprompt 包其余支撑类
- PortalBalanceRepository：缓存与刷新 credits/balance 信息。
- PortalTaskStateMonitor：轮询和调和活跃任务状态。
- PortalTaskUiSupport / PortalTaskTrajectoryUiSupport / PortalTaskScreenshotUiSupport：把状态和原始数据转成 UI 可展示文案。
- TaskPromptNotificationManager / TaskPromptNotificationActionReceiver：把任务状态映射为通知与用户动作。
- PortalAuthCallbackValidator：处理 droidrun://auth-callback 深链返回参数校验。
- 证据链：相关文件均位于 [app/src/main/java/com/droidrun/portal/taskprompt](../../app/src/main/java/com/droidrun/portal/taskprompt)

## 5. 这层为什么要单独成包
- UI 层只负责交互和展示。
- taskprompt 包负责“服务端任务”这条业务线的模型、状态机、通知、轮询与网络协议，属于完整的业务域实现。

---

本文件补齐 droidrun-portal 的 taskprompt 业务域章节。