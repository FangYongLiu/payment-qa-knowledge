---
# Scenario 对象规范(与 curation 引擎 _SKELETONS[Scenario] 对齐;人/引擎共用)。
id: scn_<name>
object_type: Scenario
name: <场景名>
aliases: []
domain: <业务域>
status: active
owner: <知识负责人=域 owner(12 域映射)>
reviewer: <评审人>
last_reviewed_at: 'YYYY-MM-DD'
source_type: <manual|wiki|cgs-apitest|...>
source_ref: <来源>
tags: []
related_services: [svc_x]            # 涉及的服务(边)
related_tables: [tbl_x]              # 落库校验的表(边)
related_logs: []
---

# <场景名>

## 触发 / 入口
- 入口 API / 操作 / 对应用例(如 cgs-apitest 用例名)。

## 关联关系
- **涉及服务**:[[svc_x]](= `related_services`)
- **校验的表**:[[tbl_x]](= `related_tables`)
- **相关日志**:`service:xxx`(= `related_logs`,排障定位用)
- **测它的接口**:[[api_x]](由 API 的 `related_scenarios` 声明,impact 反向可达,本侧不重复)
- **覆盖它的自动化**:[[auto_x]](由 AutomationAsset 的 `related_scenarios` 声明)

## 前置条件
- ...(缺则「待补」)

## 操作步骤
1. ...

## DB 校验点
- 查哪张表、哪些字段/状态(不清楚标「待补」)。

## 预期结果
- ...
> 不确定 / 缺失的点标「待补」,留待人工补充更新。
