---
# Table 对象规范。
id: tbl_<schema>_<table>
object_type: Table
name: <人类可读表名>(<物理表名>)
aliases: []
domain: <所属服务的业务域>
status: active
owner: <知识负责人=所属服务域负责人>
reviewer: <评审人>
last_reviewed_at: 'YYYY-MM-DD'
source_type: <DB 文档|wiki|...>
source_ref: <来源>
tags: []
related_services: [svc_<owning_service>]   # ★ 反指所属服务
related_scenarios: [scn_x]                  # 校验这张表的场景(可选)
---

# <表名>

## 用途
这张表存什么、属于哪个服务/业务、在什么流程里读写。

## 关联关系
- **所属服务**:[[svc_<owning>]](= frontmatter `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:[[scn_x]](= `related_scenarios`,或由 scenario 的 `related_tables` 声明)。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| ... | ... | ...（不清楚的列写「待补」） |

## 主键 / 索引
- 主键:... ;索引:...（缺则「待补:原文未提供」）

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口的一致性。
- **不确定 / 缺失的点标「待补」,留给人工补充更新。**
