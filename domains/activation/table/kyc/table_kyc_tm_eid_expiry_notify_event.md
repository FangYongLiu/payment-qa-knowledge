---
id: tbl_kyc_tm_eid_expiry_notify_event
object_type: Table
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-24'
source_type: DB DDL
source_ref: DataGrip DDL export (kyc schema) 2026-06-24
tags:
- kyc
- eid
- tm_eid_expiry_notify_event
subdomain: eid
module: null
sensitivity: normal
name: Eid有效期事件表(tm_eid_expiry_notify_event)
aliases:
- tm_eid_expiry_notify_event
related_services:
- svc_kyc
related_scenarios: []
---

# Eid有效期事件表(tm_eid_expiry_notify_event)

## 用途
**EID 有效期事件表**:跟踪 EID 过期状态与多轮过期提醒(curr_node 状态机:有效不通知→未过期通知中→已过期通知中→已过期不通知)。`relation_id` 关联流程。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 分析反向可达,本侧不重复列)。
- **哪些场景校验它**:待补(暂无直接关联场景对象)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键ID |
| `relation_id` | bigint |  | 流程记录关联ID |
| `event_type` | varchar(32) | NOT NULL | 更新有效期事件类型 |
| `member_id` | varchar(32) | NOT NULL | 会员ID |
| `status` | varchar(25) | NOT NULL | eid状态（有效，无效） |
| `expiry_date` | datetime | NOT NULL | eid有效期 |
| `partner_id` | varchar(32) |  | 平台ID |
| `eid_num` | varchar(32) |  | 用户eid |
| `curr_node` | varchar(25) | NOT NULL | 当前节点（有效不通知，未过期通知中，已过期通知中，已过期不通知） |
| `next_notify_time` | datetime |  | 下次通知时间 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |
| `version` | int | NOT NULL | 版本号 |

## 主键 / 索引
- 主键:(`id`)
- 索引 `idx_expiry_date`:(`expiry_date`)
- 索引 `idx_notify_time`:(`next_notify_time`)
- 索引 `inx_mid`:(`member_id`)

## 校验点(QA 关注)
- `curr_node` 状态机推进正确,按 `next_notify_time` 触发下一轮。
- `expiry_date` 与 OCR/ICA 的 EID 有效期一致。
- 过期后应驱动续期(renew)提示。
