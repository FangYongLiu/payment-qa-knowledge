---
id: tbl_kyc_tr_leave_record
object_type: Table
domain: kyc
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-24'
source_type: DB DDL
source_ref: DataGrip DDL export (kyc schema) 2026-06-24
tags:
- kyc
- lifecycle
- tr_leave_record
subdomain: lifecycle
module: null
sensitivity: normal
name: Leave Record Table(tr_leave_record)
aliases:
- tr_leave_record
related_services:
- svc_kyc
related_scenarios:
- scn_kyc_eid_leave
---

# Leave Record Table(tr_leave_record)

## 用途
**放弃(leave)记录表**:用户中途放弃 journey 的记录,`leave_type`(main/renew)、`category`(EID/PASSPORT)、原因。对应 leave-submit 接口。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 分析反向可达,本侧不重复列)。
- **哪些场景校验它**:[[scn_kyc_eid_leave]](= `related_scenarios`)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK | Primary Key |
| `apply_id` | bigint |  | Apply ID |
| `member_id` | varchar(20) | NOT NULL | Member ID |
| `reason` | varchar(555) | NOT NULL | Reason Description |
| `leave_type` | varchar(15) |  | Leave reason type: main/renew |
| `category` | varchar(15) |  | Category: EID/PASSPORT |
| `memo` | varchar(255) |  | Memo |
| `create_time` | timestamp | NOT NULL | Create Time |
| `update_time` | timestamp | NOT NULL | Update Time |

## 主键 / 索引
- 主键:(`id`)
- 索引 `idx_apply_id`:(`apply_id`)
- 索引 `idx_mid`:(`member_id`)

## 校验点(QA 关注)
- `category`/`leave_type` 与 journey 类型一致。
- 放弃后该 apply 不可重提(见 QA 关注点);apply_id 关联正确。
