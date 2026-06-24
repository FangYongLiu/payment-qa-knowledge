---
id: tbl_kyc_tm_pp_expiry_notify_event
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
- passport
- tm_pp_expiry_notify_event
subdomain: passport
module: null
sensitivity: normal
name: PP有效期事件表(tm_pp_expiry_notify_event)
aliases:
- tm_pp_expiry_notify_event
related_services:
- svc_kyc
related_scenarios: []
---

# PP有效期事件表(tm_pp_expiry_notify_event)

## 用途
**护照有效期事件表**:跟踪护照过期与提醒,含生效时间、缓冲宽限时间(buffer_invalid_time)、下次通知时间。`relation_id` 关联流程。

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
| `member_id` | varchar(20) | NOT NULL | 会员ID |
| `pp_no` | varchar(22) |  | 用户护照编号 |
| `status` | char | NOT NULL | 状态（Y有效，N无效） |
| `partner_id` | varchar(32) |  | 平台ID |
| `expiry_date` | datetime | NOT NULL | 护照有效期 |
| `effective_time` | datetime |  | 生效时间 |
| `buffer_invalid_time` | datetime |  | 缓冲宽限时间 |
| `next_notify_time` | datetime |  | 下次通知时间 |
| `biz_source` | varchar(155) |  | 业务来源 |
| `memo` | varchar(255) |  | 备注 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |
| `version` | int | NOT NULL | 版本号 |

## 主键 / 索引
- 主键:(`id`)
- 索引 `idx_mid`:(`member_id`)
- 索引 `idx_notify_time`:(`next_notify_time`)
- 索引 `idx_rid`:(`relation_id`)

## 校验点(QA 关注)
- `status`(Y/N) 与 expiry_date 一致;缓冲宽限期逻辑。
- `next_notify_time` 驱动提醒;与 OCR 护照有效期一致。
