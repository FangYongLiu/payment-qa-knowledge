---
id: tbl_remittance_t_sender_statics_total
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
- t_sender_statics_total
subdomain: remittance
module: null
sensitivity: normal
name: sender的汇款统计(t_sender_statics_total)
aliases:
- t_sender_statics_total
related_services:
- svc_remittance
related_scenarios: []
---
# sender的汇款统计(t_sender_statics_total)

## 用途
sender的汇款统计。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键id |
| `channel_code` | varchar(32) | NOT NULL | 渠道CODE |
| `member_id` | varchar(20) | NOT NULL | 会员id |
| `apply_counting` | int | 默认 0 | 汇款次数 |
| `success_counting` | int | 默认 0 | 汇款成功次数 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `i_statics_total_member_id` (member_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
