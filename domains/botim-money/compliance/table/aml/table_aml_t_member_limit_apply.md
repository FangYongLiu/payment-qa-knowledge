---
id: tbl_aml_t_member_limit_apply
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (aml schema) 2026-06-25
tags:
- aml
- aml
- t_member_limit_apply
subdomain: aml
module: null
sensitivity: normal
name: member limit apply table(t_member_limit_apply)
aliases:
- t_member_limit_apply
related_services:
- svc_aml
related_scenarios: []
---
# member limit apply table(t_member_limit_apply)

## 用途
member limit apply table。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | id |
| `id_no` | varchar(20) |  | id no |
| `limit_amount` | decimal(15,4) |  | limit amount |
| `currency` | char(3) | NOT NULL | currency |
| `limit_status` | char |  | limit status I-init P-processing W-wait R-reject S-success |
| `notify_status` | char |  | notify status I-init S-success F-fail |
| `memo` | varchar(255) |  | memo |
| `extension` | varchar(255) |  | extension |
| `create_time` | timestamp(3) |  | create time |
| `update_time` | timestamp(3) |  | update time |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_id_no` (id_no)
  - `idx_update_time` (update_time)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
