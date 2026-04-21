## Plan: droidrun-portal全项目源码教学分析

目标是面向“会其他语言、Kotlin/Android初学者”，对 droidrun-portal 做全量源码分析，产出工程化结果：Android架构图谱、文件级逻辑说明、Kotlin语法与Android关键API教程（绑定真实源码位置），并通过覆盖率与证据链保证可复查。

**Steps**
1. Phase A - 范围与基线
1.1 固定范围为 /home/mysic/workspace/freebie-hunting/droidrun-portal。  
1.2 先读取构建与入口元信息：settings.gradle.kts、app/build.gradle.kts、AndroidManifest.xml。  
1.3 输出“组件清单 + 权限清单 + 构建依赖清单 + 风险点”。
2. Phase B - 架构总览（Android主链路）
2.1 输出分层：UI层（Activity/Fragment）、Service层、Trigger层、Streaming层、Core层。  
2.2 输出主执行链路：应用启动 -> 权限与服务拉起 -> Socket/API接入 -> Action分发 -> Accessibility执行 -> 状态回传。  
2.3 输出状态/数据流：命令输入、事件总线、序列化消息、设备状态存储。
3. Phase C - 文件级全量讲解（按Android目录批次）
3.1 以目录分批：app/src/main/java/com/droidrun/portal/{ui,service,core,triggers,streaming,api}。  
3.2 同步覆盖 app/src/main/res（layout/drawable/values）与 AndroidManifest.xml。  
3.3 每文件固定模板：文件作用、关键类/方法、调用关系、生命周期影响、权限依赖、新手易错点。  
3.4 每批输出“已覆盖文件/未覆盖文件”清单。*可与Step 4并行滚动*
4. Phase D - Kotlin/Android教学联动（绑定真实代码）
4.1 Kotlin语法：null-safety、data class、sealed class、扩展函数、协程与suspend、Flow/StateFlow（按真实出现为准）。  
4.2 Android关键机制：Activity/Service/Receiver/AccessibilityService 生命周期与约束。  
4.3 Gradle与依赖管理：版本目录（libs.versions.toml）、模块依赖、构建变体。  
4.4 每知识点给“跨语言类比 + 最小示例 + 常见坑 + 排错建议”。
5. Phase E - 跨项目边界分析（与droidrun联动）
5.1 解释 portal 在系统中的职责边界（设备侧网关）。  
5.2 对齐协议与事件：docs/websocket-events.md、docs/local-api.md、docs/reverse-connection.md。  
5.3 指出 Python 侧对接边界：/home/mysic/workspace/freebie-hunting/droidrun/droidrun/portal.py（只讲接口边界，不展开Python实现）。
6. Phase F - 质量门禁与迭代
6.1 每条结论必须附证据：文件路径 + 符号名（类/方法/常量）。  
6.2 AI必须标注不确定项，禁止无依据推断。  
6.3 输出差距报告：盲区、争议点、下一批优先文件Top N。
7. Phase G - 最终交付
7.1 交付“droidrun-portal学习路线图”：先读Manifest，再读入口，再读Action/Service，再读触发与流媒体。  
7.2 交付“Kotlin/Android语法地图”：按项目出现频次与重要度排序。  
7.3 交付“术语表”：AccessibilityService、Foreground Service、BroadcastReceiver、Reverse Connection、WebRTC等。

**Relevant files**
- /home/mysic/workspace/freebie-hunting/droidrun-portal/app/src/main/AndroidManifest.xml — 组件入口与权限总表。
- /home/mysic/workspace/freebie-hunting/droidrun-portal/app/build.gradle.kts — 模块依赖与构建配置。
- /home/mysic/workspace/freebie-hunting/droidrun-portal/settings.gradle.kts — 工程模块定义。
- /home/mysic/workspace/freebie-hunting/droidrun-portal/gradle/libs.versions.toml — 依赖版本目录。
- /home/mysic/workspace/freebie-hunting/droidrun-portal/app/src/main/java/com/droidrun/portal/ui/MainActivity.kt — UI入口与状态面板。
- /home/mysic/workspace/freebie-hunting/droidrun-portal/app/src/main/java/com/droidrun/portal/service/DroidrunAccessibilityService.kt — UI自动化执行核心。
- /home/mysic/workspace/freebie-hunting/droidrun-portal/app/src/main/java/com/droidrun/portal/service/ActionDispatcher.kt — 指令到动作的分发枢纽。
- /home/mysic/workspace/freebie-hunting/droidrun-portal/app/src/main/java/com/droidrun/portal/service/SocketServer.kt — 连接与消息输入层。
- /home/mysic/workspace/freebie-hunting/droidrun-portal/docs/websocket-events.md — 事件协议定义。
- /home/mysic/workspace/freebie-hunting/droidrun-portal/docs/local-api.md — 本地API语义。
- /home/mysic/workspace/freebie-hunting/droidrun-portal/docs/reverse-connection.md — 反向连接设计说明。

**Verification**
1. 覆盖率检查：portal 源码文件、资源文件、文档协议文件均在已分析或明确排除清单中。
2. 证据链检查：随机抽样10条结论，验证能定位到具体文件与符号。
3. 教学有效性检查：每批至少产出3个“项目内真实 Kotlin/Android 知识点 + 最小示例 + 易错提醒”。
4. 一致性检查：架构图、生命周期链路、文件讲解和协议说明不冲突。
5. 运行语义检查：重点核对权限依赖、前台服务保活、反向连接约束是否被正确解释。

**Decisions**
- 已确认范围：droidrun-portal 全项目。
- 用户背景：会其他语言，教学输出采用跨语言类比。
- 包含内容：源码逻辑分析 + Kotlin/Android 教学联动 + 与droidrun的接口边界解释。
- 排除内容：不在本阶段修改代码或运行发布构建。

**Further Considerations**
1. 批次粒度建议：每轮处理15-30个 Kotlin 文件 + 对应资源与文档，降低上下文丢失风险。
2. 为减少幻觉，先输出“符号清单（类/方法/路由/事件）”再做解释。
3. 教学节奏建议：先组件与生命周期，再并发与网络，再协议与事件。