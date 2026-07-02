---
id: tbl_remittance_t_channel_session
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
- t_channel_session
subdomain: remittance
module: null
sensitivity: normal
name: 汇款渠道session(t_channel_session)
aliases:
- t_channel_session
related_services:
- svc_remittance
related_scenarios: []
---
# 汇款渠道session(t_channel_session)

## 用途
汇款渠道session。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 主键 |
| `channel_code` | varchar(10) | NOT NULL | 渠道code |
| `token_type` | varchar(30) | NOT NULL | 类型: bearer |
| `auth_token` | varchar(100) | NOT NULL | 渠道授权token |
| `expires_time` | datetime | NOT NULL | 到期时间 |
| `scope` | varchar(20) | NOT NULL | 作用域 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `updated_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
