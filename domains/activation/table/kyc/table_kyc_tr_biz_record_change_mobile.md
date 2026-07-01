---
id: tbl_kyc_tr_biz_record_change_mobile
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
- change-mobile
- tr_biz_record_change_mobile
subdomain: change-mobile
module: null
sensitivity: restricted
name: Change Mobile(tr_biz_record_change_mobile)
aliases:
- tr_biz_record_change_mobile
related_services:
- svc_kyc
related_scenarios: []
---

# Change Mobile(tr_biz_record_change_mobile)

## 用途
**KYC 换绑手机记录**:实名态下换绑手机,记录新旧 member_id/手机号(密文)与原 hash id。`record_id`/`req_token` 关联主流程。对应 confirm-change-mobile 接口。⚠ 当前无独立换绑场景对象(知识缺口)。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 分析反向可达,本侧不重复列)。
- **哪些场景校验它**:待补(暂无直接关联场景对象)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | Primary key ID |
| `record_id` | bigint | NOT NULL | Biz record id |
| `req_token` | varchar(32) | NOT NULL | Kyc flow token |
| `member_id` | varchar(20) | NOT NULL | Member ID |
| `mobile` | varchar(25) |  | Mobile |
| `original_hid` | varchar(25) | NOT NULL | Original hash id |
| `original_mid` | varchar(20) | NOT NULL | Original Member ID |
| `original_mobile` | varchar(25) | NOT NULL | Original mobile |
| `memo` | varchar(255) |  | Memo |
| `create_time` | timestamp | NOT NULL | Create time |
| `update_time` | timestamp | NOT NULL | Update time |

## 主键 / 索引
- 主键:(`id`)
- 索引 `idx_mid`:(`member_id`)
- 索引 `idx_rid`:(`record_id`)
- 索引 `idx_token`:(`req_token`)

## 校验点(QA 关注)
- `original_mid`/`original_mobile` 与新值差异即换绑动作;手机号密文。
- 换绑后会员态/实名态一致性;原账户处理。
- ⚠ 建议补 scn_kyc_change_mobile 场景对象覆盖此表。
