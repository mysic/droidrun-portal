# 17-Service层：高级与辅助服务

## 1. DroidrunContentProvider
- 作用：提供跨进程数据访问接口，支持触发器、状态等数据的 ContentProvider 访问。
- 关键类/方法：DroidrunContentProvider，query()/insert()/update()/delete() 等。
- 调用关系：与 TriggerRepository、StateRepository 协作，支持外部应用或脚本访问。
- 生命周期：随应用注册，进程级服务。
- 权限依赖：自定义权限、数据隔离。
- 易错点：URI 校验、权限控制、数据一致性。
- 证据链：[app/src/main/java/com/droidrun/portal/service/DroidrunContentProvider.kt](../../app/src/main/java/com/droidrun/portal/service/DroidrunContentProvider.kt)

## 2. ContentProviderAccessPolicy
- 作用：定义 ContentProvider 访问策略，限制外部访问权限与数据范围。
- 关键类/方法：ContentProviderAccessPolicy，isAccessAllowed() 等。
- 调用关系：被 DroidrunContentProvider 调用。
- 生命周期：静态策略类。
- 权限依赖：自定义权限。
- 易错点：策略兼容、权限升级。
- 证据链：[app/src/main/java/com/droidrun/portal/service/ContentProviderAccessPolicy.kt](../../app/src/main/java/com/droidrun/portal/service/ContentProviderAccessPolicy.kt)

## 3. 其他辅助服务
- HeadlessActionSupport：无界面自动化支持。
- ReverseDeviceEventRelay：反向事件转发。
- MediaProjectionAutoAccept/AutoAcceptGate/PackageInstallerAutoAccept/LocalWsNotificationActionReceiver：自动授权、通知、安装包辅助。
- 证据链：相关文件均在 service 目录下。

---

本文件为 Service 层高级与辅助服务的讲解，补全主流程外的系统集成与安全支撑模块。