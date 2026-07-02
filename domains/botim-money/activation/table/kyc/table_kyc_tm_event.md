---
id: tbl_kyc_tm_event
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
- core
- tm_event
subdomain: core
module: null
sensitivity: normal
name: 异常事件表(tm_event)
aliases:
- tm_event
related_services:
- svc_kyc
related_scenarios: []
---

# 异常事件表(tm_event)

## 用途
**异常事件表**:KYC 流程中的异常事件留痕(`relation_id` 关联流程,event_type/status/memo)。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补(暂无直接关联场景对象)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键ID |
| `relation_id` | bigint |  | 会员ID |
| `event_type` | varchar(32) |  | kyc流程token |
| `member_id` | varchar(32) |  | 会员ID |
| `status` | int |  | 本次kyc流程的状态 |
| `memo` | varchar(255) |  | 事件备注 |
| `create_time` | timestamp |  | 创建时间 |
| `updated_time` | timestamp |  | 更新时间 |
| `version` | int |  | 版本号 |

## 主键 / 索引
- 主键:(`id`)
- 索引 `idx_mid`:(`member_id`)
- 索引 `idx_relation_id`:(`relation_id`)

## 校验点(QA 关注)
- 异常事件应可回溯到 relation_id;version 乐观锁。
