---
# Flow 对象规范。
id: flow_<name>
object_type: Flow
name: <流程名>
aliases: []
domain: <业务域>
status: active
owner: <域 owner(见 index/domains.yaml)>
reviewer: <评审人>
last_reviewed_at: 'YYYY-MM-DD'
source_type: <flow_diagram|wiki|trace|...>
source_ref: <来源>
tags: []
related_services: [svc_a, svc_b]     # ★ 流程经过的服务(顺序)→ 进程级 hub,连起整条链
related_tables: []
related_scenarios: []
---

# <流程名>

## 概述
这条端到端流程做什么、起点 → 终点。

## 步骤(跨系统)
1. [[svc_a]] → [[svc_b]](做什么)...

## 关联关系
- **经过的服务(有序)**:[[svc_a]] → [[svc_b]] …(= `related_services`,串起整条链)
- **关键表**:[[tbl_x]](= `related_tables`)
- **关键场景**:[[scn_x]](= `related_scenarios`)

## 校验点
- 关键落库 / 状态流转 / 对账点(缺则「待补」)。
