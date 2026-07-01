---
id: tbl_kyc_tm_notify_record
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
- notify
- tm_notify_record
subdomain: notify
module: null
sensitivity: normal
name: 通知记录表(tm_notify_record)
aliases:
- tm_notify_record
related_services:
- svc_kyc
related_scenarios: []
---

# 通知记录表(tm_notify_record)

## 用途
**通知发送记录**:实名结果/被拒/待验证/补 EID/过期等通知的发送流水(类型/方式/次数/状态)。`relation_id` 关联流程记录。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 分析反向可达,本侧不重复列)。
- **哪些场景校验它**:待补(暂无直接关联场景对象)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键ID |
| `relation_id` | bigint | NOT NULL | KYC流程记录ID |
| `member_id` | varchar(32) |  | 会员ID |
| `uid` | varchar(32) |  | uid |
| `partner_id` | varchar(32) |  | 平台id |
| `notify_type` | varchar(32) | NOT NULL | 通知类型 0: 实名成功，1:实名被拒，2:待验证，人工审批，3:需补充EID，4：EID过期，5:其他 |
| `notify_way` | varchar(32) | NOT NULL | 通知方式 0：邮箱，1:手机短信，2:语音提示，3:公众号，4:其他 |
| `times` | int |  | 通知次数 |
| `status` | varchar(11) | NOT NULL | I：待发送，P：发送中，S：发送成功，F：发送失败 |
| `content` | varchar(512) |  | 通知内容 |
| `next_notify_time` | timestamp |  | 下次通知时间 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp |  | 更新时间 |
| `version` | int |  | 版本号 |

## 主键 / 索引
- 主键:(`id`)
- 索引 `idx_ create_time`:(`create_time`)
- 索引 `idx_member_id`:(`member_id`)
- 索引 `idx_relation_id`:(`relation_id`)

## 校验点(QA 关注)
- `status`(I/P/S/F) 流转;失败应按 `next_notify_time` 重试且 `times` 递增。
- `notify_type`/`notify_way` 与触发事件匹配;内容取自 tm_message_config。
