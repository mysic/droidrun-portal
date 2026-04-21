# 05-Trigger层：触发器管理与事件调度

## 1. TriggerApi
- 作用：触发器管理 API，提供规则增删改查、运行记录、启用禁用、测试等接口，支持本地与云端统一调用。
- 关键类/方法：TriggerApi，TriggerOperations 接口，TriggerRuntimeOperations 实现。
- 调用关系：被 ActionDispatcher、WebSocket、ReverseConnectionService 等调用，底层依赖 TriggerRuntime、TriggerRepository。
- 生命周期：随服务或 API 实例创建与销毁。
- 权限依赖：依赖具体触发源（如通知、短信、定时等）权限。
- 易错点：规则持久化、状态同步、权限兼容。
- 证据链：[app/src/main/java/com/droidrun/portal/triggers/TriggerApi.kt](../../app/src/main/java/com/droidrun/portal/triggers/TriggerApi.kt)

## 2. TriggerRepository
- 作用：触发器数据持久化，负责规则与运行记录的本地存储、迁移与查询。
- 关键类/方法：TriggerRepository，listRules()/saveRule()/deleteRule()/listRuns() 等。
- 调用关系：被 TriggerRuntime、TriggerApi 等调用，底层依赖 SharedPreferences。
- 生命周期：单例，随应用存活。
- 权限依赖：无直接权限，依赖具体触发源权限。
- 易错点：数据迁移、并发访问、存储容量。
- 证据链：[app/src/main/java/com/droidrun/portal/triggers/TriggerRepository.kt](../../app/src/main/java/com/droidrun/portal/triggers/TriggerRepository.kt)

## 3. TriggerRuntime
- 作用：触发器运行时环境，负责事件监听、规则调度、任务触发、状态同步。
- 关键类/方法：TriggerRuntime，initialize()/listRules()/listRuns()/handlePortalEvent() 等。
- 调用关系：与 EventHub、TriggerRepository、TriggerScheduler、TriggerTaskLauncher 协作。
- 生命周期：应用级单例，需初始化。
- 权限依赖：依赖具体触发源权限（如通知、短信、定时等）。
- 易错点：事件监听注册、状态同步、规则兼容。
- 证据链：[app/src/main/java/com/droidrun/portal/triggers/TriggerRuntime.kt](../../app/src/main/java/com/droidrun/portal/triggers/TriggerRuntime.kt)

## 4. TriggerAlarmReceiver
- 作用：定时触发器广播接收器，响应 AlarmManager 定时事件，驱动规则调度。
- 关键类/方法：TriggerAlarmReceiver : BroadcastReceiver，onReceive() 响应定时事件。
- 调用关系：与 TriggerScheduler、TriggerRuntime 协作。
- 生命周期：随定时任务注册与销毁。
- 权限依赖：SCHEDULE_EXACT_ALARM、定时相关权限。
- 易错点：广播注册、定时精度、系统兼容。
- 证据链：[app/src/main/java/com/droidrun/portal/triggers/TriggerAlarmReceiver.kt](../../app/src/main/java/com/droidrun/portal/triggers/TriggerAlarmReceiver.kt)

---

本文件为 Trigger 层触发器管理与事件调度相关组件的详细讲解，后续将继续补充 Streaming、Core、API 层文件。