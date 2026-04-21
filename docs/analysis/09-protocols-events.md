# 09-协议与事件机制

## 1. WebSocket 事件协议
- 作用：Portal 内置 WebSocket 服务器，推送设备实时事件（通知、应用切换、电量、网络、短信等）。
- 事件类型：NOTIFICATION、APP_ENTERED、BATTERY_LOW、USER_PRESENT、NETWORK_CONNECTED、SMS_RECEIVED 等。
- 事件格式：{"type": "EVENT_TYPE", "timestamp": ..., "payload": {...}}
- 支持 JSON-RPC 风格命令，详见 local-api.md。
- 证据链：[docs/websocket-events.md](../websocket-events.md)

## 2. 本地 API 与反向连接协议
- 作用：支持 HTTP/WebSocket/ContentProvider 本地控制，设备可主动连接云端实现 NAT 穿透。
- 方法示例：tap、swipe、global、app、keyboard/input、screenshot、packages、state、install 等。
- 反向连接：设备主动连接云端 WebSocket，协议与本地一致，支持事件推送与触发器管理。
- 证据链：[docs/local-api.md](../local-api.md)、[docs/reverse-connection.md](../reverse-connection.md)

## 3. 触发器与事件管理协议
- 作用：支持触发器增删改查、启用禁用、测试、运行记录等，统一 TriggerJson schema。
- 方法示例：triggers/catalog、triggers/status、triggers/rules/list、triggers/rules/save、triggers/runs/list 等。
- 证据链：[docs/triggers.md](../triggers.md)

---

本文件为 droidrun-portal 主要协议与事件机制的概览，结合源码与文档，便于理解系统对外能力与集成方式。