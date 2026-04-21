# 13-差距报告与下一步计划

## 1. 盲区与争议点
- `app/src/main` 下的 Application、Manifest、res、各一级业务包已完成覆盖；当前未纳入主讲解的主要是测试代码与辅助脚本。
- 测试代码与脚本（如 `test_websocket.py`、`scripts/check_event_streams.py`）仍未纳入主教程。
- 三方依赖库源码未展开，仅分析了 Portal 对这些依赖的接口调用与使用方式。

## 2. 下一批优先文件 Top N
1. 测试与脚本代码（`test_websocket.py`、`scripts/check_event_streams.py`）
2. `build/` 之外的工程化支撑文件，如 Gradle 包装、发布与版本策略
3. 依赖库升级与兼容性分析
4. 结合实际运行日志与用户反馈补充易错点
5. 为关键主链路补更多时序图与交互图

## 3. 持续改进建议
- 定期复查主链路与协议兼容性，跟进新版本变更。
- 若需要进一步扩大覆盖范围，下一步应转向测试、脚本与构建链路，而不是 `app/src/main` 主体源码。
- 增加更多跨语言对比与实战案例。

---

本文件为 droidrun-portal 教学分析的差距报告与后续计划，便于持续完善与扩展。