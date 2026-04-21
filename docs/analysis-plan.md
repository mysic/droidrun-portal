# droidrun-portal 全项目源码教学分析规划

## 1. 范围与基线
- 固定范围为 droidrun-portal 全项目。
- 读取 settings.gradle.kts、app/build.gradle.kts、AndroidManifest.xml，输出组件清单、权限清单、构建依赖清单、风险点。

## 2. 架构总览
- 分层：UI层、Service层、Trigger层、Streaming层、Core层、API层。
- 主执行链路：应用启动 -> 权限与服务拉起 -> Socket/API接入 -> Action分发 -> Accessibility执行 -> 状态回传。
- 状态/数据流：命令输入、事件总线、序列化消息、设备状态存储。

## 3. 文件级全量讲解
- 按目录分批：app/src/main/java/com/droidrun/portal/{ui,service,core,triggers,streaming,api}。
- 每文件固定模板：文件作用、关键类/方法、调用关系、生命周期影响、权限依赖、新手易错点。
- 每批输出“已覆盖文件/未覆盖文件”清单。

## 4. Kotlin/Android 教学联动
- 结合真实源码讲解 Kotlin 语法与 Android 关键机制。
- 每知识点给“跨语言类比 + 最小示例 + 常见坑 + 排错建议”。

## 5. 跨项目边界分析
- 解释 portal 在系统中的职责边界。
- 对齐协议与事件文档。
- 指出 Python 侧对接边界。

## 6. 质量门禁与交付
- 每条结论附证据链（文件路径+符号名）。
- 输出差距报告与下一批优先文件。
- 交付学习路线图、语法地图、术语表。

---

本文件为教学分析全流程规划，后续所有分析与教程均以此为基准，分阶段推进。