---
id: tbl_member_tm_kyc_correct_his
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (member schema) 2026-06-25
tags:
- member
- kyc-verify
- tm_kyc_correct_his
subdomain: kyc-verify
module: null
sensitivity: normal
name: 实名信息更正历史表(tm_kyc_correct_his)
aliases:
- tm_kyc_correct_his
related_services:
- svc_member
related_scenarios: []
---

# 实名信息更正历史表(tm_kyc_correct_his)

## 用途
实名信息更正历史表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK | 主键 |
| `kyc_type` | varchar(22) | NOT NULL | kyc类型 |
| `entity_id` | varchar(22) | NOT NULL | 实名记录ID |
| `member_id` | varchar(22) | NOT NULL | 会员ID |
| `original_data` | varchar(800) | NOT NULL | 原数据集 |
| `updated_data` | varchar(800) | NOT NULL | 更新数据集 |
| `operator` | varchar(50) |  | 操作员 |
| `document_tag` | varchar(80) |  | 附件tag |
| `memo` | varchar(128) |  | 备注 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
