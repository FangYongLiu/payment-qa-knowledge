---
id: tbl_remittance_t_beneficiary_statics_total
object_type: Table
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (remittance schema) 2026-06-25
tags:
- remittance
- remittance
- t_beneficiary_statics_total
subdomain: remittance
module: null
sensitivity: normal
name: 受益人统计表(t_beneficiary_statics_total)
aliases:
- t_beneficiary_statics_total
related_services:
- svc_remittance
related_scenarios: []
---
# 受益人统计表(t_beneficiary_statics_total)

## 用途
受益人统计表。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `statics_id` | bigint | PK / NOT NULL | 主键 |
| `member_id` | varchar(20) | NOT NULL | 会员id |
| `beneficiary_count` | int |  | 当前受益人数量 |
| `del_count` | int |  | 已删除的受益人数量 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`statics_id`)
- 索引:
  - `idx_member_id` (member_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
