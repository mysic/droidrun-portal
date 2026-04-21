# 25-main 源码覆盖索引

本文件用于把 `app/src/main` 的源码与资源目录逐项映射到 analysis 章节，方便快速确认覆盖范围。

## 1. Java/Kotlin 源码包覆盖
- `PortalApplication.kt` -> [21-application-config-events.md](21-application-config-events.md)
- `api/` -> [08-api-layer.md](08-api-layer.md)
- `config/` -> [21-application-config-events.md](21-application-config-events.md)
- `core/` -> [07-core-layer.md](07-core-layer.md)
- `events/` 与 `events/model/` -> [21-application-config-events.md](21-application-config-events.md)
- `input/` -> [22-input-model-state.md](22-input-model-state.md)
- `keepalive/` -> [20-keepalive-module.md](20-keepalive-module.md)
- `model/` -> [22-input-model-state.md](22-input-model-state.md)
- `service/` 核心执行链 -> [03-service-accessibility-action-socket.md](03-service-accessibility-action-socket.md)、[04-service-reverse-screen-notification.md](04-service-reverse-screen-notification.md)
- `service/` 辅助与高级模块 -> [15-utils-and-helpers.md](15-utils-and-helpers.md)、[17-service-advanced.md](17-service-advanced.md)
- `state/` -> [22-input-model-state.md](22-input-model-state.md)
- `streaming/` -> [06-streaming-layer.md](06-streaming-layer.md)
- `taskprompt/` -> [23-taskprompt-domain.md](23-taskprompt-domain.md)
- `triggers/` 核心 -> [05-trigger-layer.md](05-trigger-layer.md)
- `triggers/` 辅助与高级模块 -> [18-trigger-advanced.md](18-trigger-advanced.md)
- `ui/MainActivity.kt`、`ui/ScreenCaptureActivity.kt` -> [01-ui-mainactivity-screencapture.md](01-ui-mainactivity-screencapture.md)
- `ui/settings/`、`ui/taskprompt/TaskPromptCardController.kt`、`ui/taskprompt/TaskDetailsActivity.kt` -> [02-ui-settings-taskprompt.md](02-ui-settings-taskprompt.md)
- `ui/triggers/`、`ui/taskprompt/TaskHistoryActivity.kt` -> [16-ui-trigger-taskhistory.md](16-ui-trigger-taskhistory.md)
- `ui/overlay/OverlayManager.kt`、`ui/EditTextExtensions.kt` -> [15-utils-and-helpers.md](15-utils-and-helpers.md)
- `ui/PermissionDialogActivity.kt`、`ui/taskprompt/TaskPromptSettingsPanelController.kt` -> [19-ui-remaining.md](19-ui-remaining.md)

## 2. Manifest 与资源覆盖
- `AndroidManifest.xml` -> [24-manifest-and-resources.md](24-manifest-and-resources.md)
- `res/layout/` -> [24-manifest-and-resources.md](24-manifest-and-resources.md)
- `res/drawable/` -> [24-manifest-and-resources.md](24-manifest-and-resources.md)
- `res/mipmap-*/` -> [24-manifest-and-resources.md](24-manifest-and-resources.md)
- `res/values/` 与 `res/values-night/` -> [24-manifest-and-resources.md](24-manifest-and-resources.md)
- `res/xml/` -> [24-manifest-and-resources.md](24-manifest-and-resources.md)

## 3. 总体结论
- 以 `app/src/main` 为边界，当前 analysis 已覆盖全部一级源码包、Application 入口、Manifest 与资源目录。
- 当前未纳入本索引的内容不属于 `main` 主体源码范围，主要是测试、脚本与构建辅助文件。

---

本文件是 `app/src/main` 与 analysis 教程之间的覆盖映射表。