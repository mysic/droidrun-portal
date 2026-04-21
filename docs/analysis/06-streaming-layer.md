# 06-Streaming层：WebRtcManager 与 ScrcpyControlChannel

## 1. WebRtcManager
- 作用：WebRTC PeerConnection 管理器，负责流媒体会话、信令、推流、ICE 管理等，支持本地与云端屏幕投屏。
- 关键类/方法：WebRtcManager 单例，getInstance()/shutdown()，内部 PeerConnection/Session 管理。
- 调用关系：与 ScreenCaptureService、ReverseConnectionService 协作，驱动屏幕流媒体推送。
- 生命周期：应用级单例，随投屏需求创建与销毁。
- 权限依赖：MediaProjection、网络。
- 易错点：ICE 协议兼容、会话管理、资源释放。
- 证据链：[app/src/main/java/com/droidrun/portal/streaming/WebRtcManager.kt](../../app/src/main/java/com/droidrun/portal/streaming/WebRtcManager.kt)

## 2. ScrcpyControlChannel
- 作用：WebRTC DataChannel 控制通道，支持远程注入触摸、按键、文本、剪贴板、面板操作等，兼容 scrcpy 协议。
- 关键类/方法：ScrcpyControlChannel : DataChannel.Observer，onMessage()/handleMessage()/handleTouch()/handleKeycode() 等。
- 调用关系：与 WebRtcManager、DroidrunAccessibilityService、GestureController 协作，驱动远程控制。
- 生命周期：随 WebRTC 会话创建与销毁。
- 权限依赖：Accessibility、输入、剪贴板等。
- 易错点：协议兼容、数据解析、手势注入。
- 证据链：[app/src/main/java/com/droidrun/portal/streaming/ScrcpyControlChannel.kt](../../app/src/main/java/com/droidrun/portal/streaming/ScrcpyControlChannel.kt)

---

本文件为 Streaming 层流媒体与远程控制相关组件的详细讲解，后续将继续补充 Core、API 层文件。