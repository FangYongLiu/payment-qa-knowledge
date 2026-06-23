---
# Domain 对象规范(与 _SKELETONS[Domain] 对齐)。
id: domain_<slug>
object_type: Domain
name: <业务域名称>
aliases: []
domain: <slug 自身>
status: active
owner: <域 owner(12 域映射)>
reviewer: <评审人>
last_reviewed_at: 'YYYY-MM-DD'
source_type: <manual|wiki|...>
source_ref: <来源>
tags: []
related_services: []
---

# <业务域>

## 概述
这个业务域做什么、边界。

## 覆盖范围
- 子域 / 模块 / 关键能力。

## 关联关系
- **关键服务**:[[svc_x]](= `related_services`)
- **关键流程**:[[flow_x]](本域的端到端流程对象)

## QA 关注点
- 该域测试重点、易错点(缺则「待补」)。
