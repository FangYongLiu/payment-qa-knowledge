---
id: tbl_aml_t_sms_record
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
- t_sms_record
subdomain: aml
module: null
sensitivity: normal
name: 短信记录(t_sms_record)
aliases:
- t_sms_record
related_services:
- svc_aml
related_scenarios: []
---
# 短信记录(t_sms_record)

## 用途
短信记录。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `cis_ticket` | varchar(100) | NOT NULL | 系统生成唯一票据,校验结果时用 |
| `otp_ticket` | varchar(100) | NOT NULL | otp返回的票据 |
| `otp_token` | varchar(100) | NOT NULL | 客户端token |
| `verify_result` | tinyint(2) | 默认 0 | 校验结果-0.失败；1.通过； |
| `failure_times` | smallint | 默认 0 | 失败次数 |
| `create_time` | timestamp | 默认 CURRENT_TIMESTAMP | 创建时间 |
| `update_time` | timestamp | 默认 CURRENT_TIMESTAMP | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_sms_record_otp_ticket` (otp_ticket)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
