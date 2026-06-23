---
# Troubleshooting 对象规范(与 _SKELETONS[Troubleshooting] 对齐)。
id: ts_<symptom>
object_type: Troubleshooting
name: <现象简述>
aliases: []
domain: <业务域>
status: active
owner: <域 owner(12 域映射)>
reviewer: <评审人>
last_reviewed_at: 'YYYY-MM-DD'
source_type: <rca|wiki|...>
source_ref: <来源>
tags: []
related_services: [svc_x]
related_tables: [tbl_x]
related_logs: []
related_failures: []
---

# <现象>

## 症状
用户 / 系统看到什么。

## 关联关系
- **涉及服务 / 表**:[[svc_x]] / [[tbl_x]](= `related_services` / `related_tables`)
- **相关日志**:`service:xxx`(= `related_logs`)
- **关联故障 / 历史案例**:[[ts_x]](= `related_failures`)

## 可能根因
- ...(related_failures)

## 排查步骤
- DB:查哪张表 / 字段;Kibana:看哪个服务日志、关键字(related_logs)。

## 处理 / 规避
- 怎么修 / 绕过;相似历史案例链接。
> 不确定的标「待补」。
